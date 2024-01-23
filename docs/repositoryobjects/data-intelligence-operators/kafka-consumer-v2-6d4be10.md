<!-- loio6d4be1097f8d4df0b18e3a606ae9b607 -->

# Kafka Consumer V2

The Kafka Consumer operator works as a Kafka client that consumes records or messages from a Kafka cluster. It is compatible with Kafka versions 0.9.x and later.



<a name="loio6d4be1097f8d4df0b18e3a606ae9b607__section_sq1_nf3_vdb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

ID

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Connection

</td>
<td valign="top">

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. The object containing the connection parameters to a KAFKA instance.

Default: \{\}

</td>
</tr>
<tr>
<td valign="top">

Kafka Version

</td>
<td valign="top">

kafkaVersion

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The version of Kafka server being used.

Default: "1.0.0"

</td>
</tr>
<tr>
<td valign="top">

Topics

</td>
<td valign="top">

topics

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Name of the topics from which messages are read and sent to the pipeline \(consumed\). Topic names are separated by `,`.

Default: "test\_topic"

</td>
</tr>
<tr>
<td valign="top">

Auto Commit

</td>
<td valign="top">

autoCommit

</td>
<td valign="top">

bool

</td>
<td valign="top">

Whether to automatically commit the message \(mark message as processed\). When this configuration is enabled and snapshot is not used, each message is committed right after it is sent to the output port. On the **Snapshot Support** session, there are more details about how this configuration works with snapshot feature. Once a message is committed, it will not be consumed anymore, and it is removed from the queue.

Default: true

</td>
</tr>
<tr>
<td valign="top">

Max Wait Time

</td>
<td valign="top">

maxWaitTime

</td>
<td valign="top">

int

</td>
<td valign="top">

The maximum amount of time in milliseconds that the broker waits for the consumer.

Default: 500

</td>
</tr>
<tr>
<td valign="top">

Retry Attempts

</td>
<td valign="top">

numRetryAttempts

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of attempts to retry.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Offset

</td>
<td valign="top">

offset

</td>
<td valign="top">

string

</td>
<td valign="top">

The initial offset to use if no offset was previously commited.

Default: "newest"

</td>
</tr>
<tr>
<td valign="top">

Isolation Level

</td>
<td valign="top">

isolationLevel

</td>
<td valign="top">

string

</td>
<td valign="top">

Controls how the consumer reads transactional messages. If set to `Read Committed`, only transactional messages that have been committed are read. If set to `` \(default\), all messages, including transactional messages that have been aborted, are read. Non-transactional messages are read in either mode.

Default: "Read Uncommitted"

</td>
</tr>
<tr>
<td valign="top">

Maintain Full Metadata Set

</td>
<td valign="top">

fullMetadataSet

</td>
<td valign="top">

bool

</td>
<td valign="top">

Whether to maintain a full set of metadata for all topics in the Kafka cluster or just the minimal set necessary. If there are many topics and partitions, it is recommended to disable this option.

Default: true

</td>
</tr>
<tr>
<td valign="top">

Error Handling

</td>
<td valign="top">

errorHandling

</td>
<td valign="top">

string

</td>
<td valign="top">

Whether to terminate the consumer in case the Kafka Consumer throws an error.

Default: "terminate on error"

</td>
</tr>
</table>



<a name="loio6d4be1097f8d4df0b18e3a606ae9b607__section_knq_5f3_vdb"/>

## Input


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`markoffset` 

</td>
<td valign="top">

message

</td>
<td valign="top">

An input with an empty body the com.sap.headers.kafka header. Only the fields topic, partition, and offset are necessary. This data is used to mark the related message as processed \(committed\).

</td>
</tr>
</table>



<a name="loio6d4be1097f8d4df0b18e3a606ae9b607__section_swc_cg3_vdb"/>

## Output


<table>
<tr>
<th valign="top">

Output

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`message` 

</td>
<td valign="top">

message

</td>
<td valign="top">

A binary output containing the consumed content in the body and com.sap.headers.kafka headers.

</td>
</tr>
<tr>
<td valign="top">

`event`

</td>
<td valign="top">

message

</td>
<td valign="top">

A binary output containing, in the body, the stream of notifications produced by the consumer, such as rebalance notifications.

</td>
</tr>
</table>



<a name="loio6d4be1097f8d4df0b18e3a606ae9b607__section_rnt_r5v_nsb"/>

## Snapshot Support

Snapshot support is provided when `AutoCommit` is set to **True**, and `Offset` is set to **oldest**. When it is enabled, consumed messages will only be committed on epoch completion. Since the Kafka Server keeps track of uncommitted messages, there is no recovery functionality implemented on the operator itself. Uncommitted messages will be automatically recovered by the server.

