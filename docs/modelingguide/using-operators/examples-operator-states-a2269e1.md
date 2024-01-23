<!-- loioa2269e1442834a61997573f1bfb45827 -->

# Examples: Operator States

This section contains examples illustrating the use of state management functions in the Python3 operator for graph snapshots and operator states for Gen2 graphs.



<a name="loioa2269e1442834a61997573f1bfb45827__section_gty_v42_5vb"/>

## Exactly Once Graph Structure

The following example uses this exactly-once graph structure:

```
PythonOperator Generator > Deterministic Processing > Idempotent Writer
```

Assumptions:

-   The example doesn't include instances of the processing operator because the processing operator can perform any operation, stateful or not, as long as it's deterministic. Therefore, if the graph is fed with the same inputs, the same outputs are expected.
-   The graph has a linear topology, which means that the operators don't have to fan in or out messages.
-   The PythonOperator Generator accesses an SAP HANA table to which the system appended its content during the graph execution.

> ### Example:  
> The following code snippet shows the script:
> 
> ```
> ''' python
>     from hdbcli import dbapi
> 
> offset = 0
> c = None
> 
> api.set_initial_snapshot_info(api.InitialProcessInfo(is_stateful=True,outports_info={'output': api.OutportInfo(is_generator=True)}))
> 
> # Operator will have batches and it will be Replayable
> def prestart():
>     conn = dbapi.connect(
>         address=api.config.connection['connectionProperties']['host'],
>         port=api.config.connection['connectionProperties']['port'],
>         user=api.config.connection['connectionProperties']['user'],
>         password=api.config.connection['connectionProperties']['password'],
>         sslHostNameInCertificate='*',
>         sslValidateCertificate=False
>     )
>     global c
>     c = conn.cursor()
>     
> def time_callback():
>     global offset
>     # The order by guarantees the same order when replaying
>     c.execute(f"SELECT * FROM test ORDER BY x LIMIT 2 OFFSET {offset};")
>     test_data = c.fetchall()
>     c.close()
>     offset += 2
>     if len(test_data) > 0:
>         t = [[entry for entry in row] for row in test_data]
>         api.outputs.output.publish(api.Table(t))
>     return 0
> 
> api.add_timer(time_callback)
>     
> api.set_prestart(prestart)
> 
> # Since we assume new entries will go to the end of the table, we can only save the offset
> # and not the table.
> def serialize(epoch):
>     return pickle.dumps(offset)
> 
> api.set_serialize_callback(serialize)
> 
> def restore(epoch, state_bytes):
>     global offset
>     offset = pickle.loads(state_bytes)
> 
> api.set_restore_callback(restore)
> 
> 
> ```



### Idempotent Writer Script

> ### Example:  
> Continuing with Example 1, the idempotent writer also writes to an SAP HANA table through the following script:
> 
> ```
> from hdbcli import dbapi
> 
> offset = 0
> c = None
> 
> def prestart():
>     conn = dbapi.connect(
>         address=api.config.connection['connectionProperties']['host'],
>         port=api.config.connection['connectionProperties']['port'],
>         user=api.config.connection['connectionProperties']['user'],
>         password=api.config.connection['connectionProperties']['password'],
>         sslHostNameInCertificate='*',
>         sslValidateCertificate=False
>     )
>     global c
>     c = conn.cursor()
>     
> def on_input(msg_id, header, body):
>     data = body.get().body
>     
>     # Upsert guarantees idempotency
>     sql = 'UPSERT test (x, y, z) VALUES (?, ?, ?) where x=?'
>     for row in data:
>         row.append(row[0])
>         c.execute(sql, row)
>     c.close()
>     
> api.set_port_callback("input", on_input)
> 
> api.set_prestart(prestart)
> 
> ```



<a name="loioa2269e1442834a61997573f1bfb45827__section_gxs_ssy_5vb"/>

## No Idempotent Guarantee

> ### Example:  
> The following example uses the same setup as the Exactly Once Graph Structure example, but the writer isn't guaranteed to be idempotent. To have the exactly once guarantees, the graph has to avoid writing duplicate batches through an auxiliary table in the same SAP HANA database.
> 
> The auxiliary table can be another persistence structure. In this example, the auxiliary table is a Write-Ahead Log \(WAL\). To preserve already seen batches, the table has to survive multiple-graph runs. Therefore, create and delete the WAL outside the graph context.
> 
> The following script shows the implementation of the generator and writers as Python Operators:
> 
> ```
> ''' python
> from hdbcli import dbapi
> import pickle
> 
> offset = 0
> ID = 0
> c = None
> # Table is broken into messages of 100 rows, and each made of 10 batches fo 10 rows
> batch_size = 10
> message_size = 100
> 
> api.set_initial_snapshot_info(api.InitialProcessInfo(is_stateful=True,outports_info={'output': api.OutportInfo(is_generator=True)}))
> 
> def prestart():
>     conn = dbapi.connect(
>         address=api.config.connection['connectionProperties']['host'],
>         port=api.config.connection['connectionProperties']['port'],
>         user=api.config.connection['connectionProperties']['user'],
>         password=api.config.connection['connectionProperties']['password'],
>         sslHostNameInCertificate='*',
>         sslValidateCertificate=False
>     )
>     global c
>     c = conn.cursor()
>     
> final = False
> def time_callback():
>     global offset, ID
>     # The order by guarantees the same order when replaying
>     c.execute(f"SELECT * FROM test ORDER BY x LIMIT {batch_size} OFFSET {offset};")
>     test_data = c.fetchall()
>     c.close()
>     global final
>     if len(test_data) > 0 and not final:
>         api.logger.info('sending1')
>         t = [[entry for entry in row] for row in test_data]
>         h = {}
>         if len(test_data) < batch_size:
>             h['isFinal'] = [True]
>             final = True
>         else:
>             h['isFinal'] = [False]
>         h['batchNum'] = [offset // batch_size]
>         h['messageNum'] = [offset // message_size ]
> 
>         # The last batch has the flag set to true, this is important so the writer operator can clean up the WAL
>         if (offset + batch_size) % message_size == 0 and offset > 1:
>             h['isFinal'] = [True]
>         
>         h['ID'] = [ID]
>         api.outputs.output.publish(api.Table(t), h)
>         api.logger.info('after')
>         ID += 1
>         offset += batch_size
>     return 0
> 
> api.add_timer(time_callback)
>     
> api.set_prestart(prestart)
> 
> # Since we assume new entries will go to the end of the table, we can only save the offset
> # and not the table.
> def serialize(epoch):
>     return pickle.dumps([offset, ID])
> 
> api.set_serialize_callback(serialize)
> 
> def restore(epoch, state_bytes):
>     global offset, ID
>     offset, ID = pickle.loads(state_bytes)
>     
> 
> api.set_restore_callback(restore)
> 
> ```



### Idempotent Guarantee That Accesses SAP HANA Table

> ### Example:  
> The writer also accesses an SAP HANA table in the following script:
> 
> ```
> ''' python
> import pickle
> from hdbcli import dbapi
> 
> offset = 0
> messages_done = {}
> c = None
> 
> api.set_initial_snapshot_info(api.InitialProcessInfo(is_stateful=True))
> 
> def prestart():
>     conn = dbapi.connect(
>         address=api.config.connection['connectionProperties']['host'],
>         port=api.config.connection['connectionProperties']['port'],
>         user=api.config.connection['connectionProperties']['user'],
>         password=api.config.connection['connectionProperties']['password'],
>         sslHostNameInCertificate='*',
>         sslValidateCertificate=False
>     )
>     global c
>     c = conn.cursor()
> 
>     
> def insert_wal(ID, batch_num, message_num):
>     sql = 'INSERT INTO WAL VALUES(?,?,?)'
>     c.execute(sql, [ID, batch_num, message_num])
>     c.close()
>     
> def is_batch_new(batch_num, message_num):
>     c.execute(f'SELECT ID FROM WAL WHERE BATCH={batch_num} AND MESSAGE={message_num}')
>     test_data = c.fetchall()
>     c.close()
>     return len(test_data) == 0
>     
> def on_input(msg_id, header, body):
>     api.logger.info('Receiving')
>     data = body.get().body
>     
>     batch_num = header['batchNum'][0]
>     message_num = header['messageNum'][0]
>     
>     if header['isFinal'][0]:
>         api.logger.info('Final message')
>         global messages_done
>         messages_done[message_num] = None
>     
>     # It will check if messageID and batchID do not exist in the WAL table, if they do, message is ignored
>     if not is_batch_new(batch_num, message_num):
>         return
>     
>     api.logger.info('Inserting into test2')
>     sql = 'INSERT INTO test2 (x, y, z) VALUES (?, ?, ?)'
>     for row in data:
>         row.append(row[0])
>         c.execute(sql, row)
>     c.close()
>     
>     api.logger.info('Inserting into wal')
>     # Insert into WAL table, and if message is done, insert accordingly
>     insert_wal(header['ID'][0], batch_num, message_num)
>     
>     api.logger.info('sending to output')
>     api.outputs.output.publish(str(data))
>     
> 
> api.set_port_callback("input", on_input)
> 
> api.set_prestart(prestart)
> 
> # Any messages that have been finished by this point are eligible to be removed from
> # WAL when the epoch is completed.
> def serialize(epoch):
>     global messages_done
>     api.logger.info(f'setting epochs {messages_done}')
>     for messageID, val in messages_done.items():
>         if val is None:
>             messages_done[messageID] = epoch
>     
>     # The writer has to keep as state the map, since finished messages may not have had their epochs processed
>     return pickle.dumps(messages_done)
> 
> api.set_serialize_callback(serialize)
> 
> def restore(epoch, state_bytes):
>     global messages_done
>     messages_done = pickle.loads(state_bytes)
> 
> api.set_restore_callback(restore)
> 
> # Any message whose corresponding epoch existing could
> # be removed as we know the epoch has finished
> def complete_callback(epoch):
>     global messages_done
>     api.logger.info(f'removing from wal {messages_done}')
>     for messageID, e in messages_done.items():
>         if e == epoch:
>             api.logger.info(f'removing message {messageID}')
>             c.execute(f'DELETE FROM WAL WHERE MESSAGE=?', [messageID])
>             c.close()
> 
>             # cleaning up ended epochs
>             del messages_done[messageID]
> 
> api.set_epoch_complete_callback(complete_callback)
> ```
> ```

