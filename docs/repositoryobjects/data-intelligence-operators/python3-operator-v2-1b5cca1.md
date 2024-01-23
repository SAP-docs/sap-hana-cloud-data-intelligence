<!-- loio1b5cca1e8f3f418593d042661cc135ad -->

# Python3 Operator V2

Use the Python3 operator V2 to define a script that offers convenience functions provided by API objects, such as callbacks.



> ### Example:  
> Set a callback function that the operator calls when it receives new data in the “datain” port by writing `api.set_port_callback("datain", callback_name)`.

You can create an operator that extends the Python3 operator directly in the *Repository* tab of the Modeler application. For more information about extensions, see the [Operator Details](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/2a647f3e65454a1b9e0b66c393bed530.html "Every operator has an ID (also known as name) and a title (also known as the description). The operator ID is a unique identifier, with a strict format. The operator title is what the graphical interface displays.") :arrow_upper_right: topic in the *Modeling Guide*.

> ### Note:  
> This Python3 operator V2 runs on Python 3.9.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_sq1_nf3_vdb"/>

## Configuration Parameters

The following table describes the Python3 operator V2 configuration parameters.


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Description

</th>
<th valign="top">

ID

</th>
<th valign="top">

Type

</th>
</tr>
<tr>
<td valign="top">

**Script**

</td>
<td valign="top">

Required. The inline script to execute. If the script starts with “file://”, the operator runs the script file.

The default value is `""`.

</td>
<td valign="top">

script

</td>
<td valign="top">

string

</td>
</tr>
<tr>
<td valign="top">

**Error Handling**

</td>
<td valign="top">

Required. Defines how the operator handles exceptions during prestart, port callbacks, and timer callbacks.

If not previously triggered, an exception terminates the graph run during shutdown.

Accepted values are as follows:

-   `terminate on error`: When the operator throws an exception, the graph terminates. `Terminate on error` is the default value.
-   `log and ignore`: When the operator throws an exception, it logs the exception and continues running.
-   `propagate to error port`: When the operator throws an exception, it sends the exception to the error port and continues running.

    The operator assumes there's an existing port named `error`, of types `structure` and `com.sap.error`.

    To provide more details, such as `code`, `text`, and `details`, create a custom exception named `api.OperatorException(code: int, text: str, details: api.Table)`.

-   `retry`: When the operator throws an exception, it communicates the exception through response callback.

For more information, see the [Error Handling](python3-operator-v2-1b5cca1.md#loio1b5cca1e8f3f418593d042661cc135ad__section_a1z_m25_zdb) section.

</td>
<td valign="top">

errorHandling

</td>
<td valign="top">

string

</td>
</tr>
</table>



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_knq_5f3_vdb"/>

## Input

None.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_swc_cg3_vdb"/>

## Output

None.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_gd5_pd5_zdb"/>

## Basic Examples

> ### Example:  
> The following code snippet counts all incoming messages on the port named “input” \(of arbitrary type\), and writes the count to the port named “output” \(type scalar, "com.sap.core.int64"\):
> 
> ```
> counter = 0
> 
> def on_input(msg_id, header, data):
>     global counter
>     counter += 1
>     api.outputs.output.publish(counter)
> 
> api.set_port_callback("input", on_input)
> ```
> 
> Because the variable `counter` is the Python type `int`, the port “output” for an operator that contains the example code snippet is of type `com.sap.core.int*`.

For more information on how to choose your port types, see the [Correspondence Between Core Scalars and Python Types](python3-operator-v2-1b5cca1.md#loio1b5cca1e8f3f418593d042661cc135ad__section_qm4_jf5_zdb) section.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_ndj_jtk_lpb"/>

## api.outputs.port.publish\(data, header=None, response\_callback=None\)

This API publishes 'data' and 'header' to the outport named 'port'.

Output is possible only after the operator initializes; during prestart, timer, and port callbacks.

**Arguments:**


<table>
<tr>
<td valign="top">

`data (...)`

</td>
<td valign="top">

The data to send.

</td>
</tr>
<tr>
<td valign="top">

`header (header|dict optional)`

</td>
<td valign="top">

The dictionary mapping 'header name'-\> \['header content'\]. You can also use 'header' type from port callbacks. If there's no header provided, the operator uses an empty header as default.

</td>
</tr>
<tr>
<td valign="top">

`response_callback(func[msg_id, ex], optional)`

</td>
<td valign="top">

The callback that the operator calls after the next operator receives and processes the message correctly. Values include the following:

-   `'msg_id'` identifies the message and matches the return from the publish functions.
-   `'ex'` is an exception when there's one or 'none'. `'ex'` comes from the message processing of the next operator. If there's no `response_callback` and the value of `'ex'` is None, the default function raises an exception.



</td>
</tr>
</table>

**Returns** 

`msg_id (bytes)`: 12-byte message unique identifier in a port-specific connection.

> ### Example:  
> ```
> # For this example, you need to create an input port of arbitrary type
> # and an output port of the same type and type-id.
> import datetime
> 
> # Instead of raising an exception like the default, this custom only logs
> def custom_response_callback(msg_id, ex):
>     if ex:
>         api.logger.error("Error when publishing %s: %s" % (str(msg_id), str(ex)))
> 
> def on_input(msg_id, header, body):
> 
>     # Access single headers as dictionary and check if they are present
>     # to avoid errors
>     if 'header.type.id' in header:
>         header_val = header['header.type.id']
> 
>     # Read body value when not stream
>     body_val = body.get()
> 
>     # Body cannot be directly sent, use the value instead
>     # Header can be directly sent, it also possible to copy it (.copy())
>     api.outputs.output.publish(body_val, header)
>     
>     # New Headers can be a list or api.Record of the header's structure fields
>     new_header = api.Record([
>       "dummyConnection", # connection
>       "dummy/Path", # path
>       0, # size
>       False, #isDir
>       datetime.datetime.now().isoformat() # modTime
>     ])
>     
>     # For the output you need to create as specified a dict of single headers
>     # key: type-id of the single header
>     # value: list / api.Record of the header's structure fields
>     new_out_headers = {"com.sap.headers.file": new_header}
> 
>     # Also possible to send new header and body and response callback
>     # Body should match the port type
>     api.outputs.output.publish(body_val, new_out_headers, custom_response_callback)
> 
> api.set_port_callback("input", on_input)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_dvk_5tk_lpb"/>

## api.outputs.port.publish\(binary\_data, n, header=None, response\_callback=None\)

This API publishes the first `'n'` bytes from `'data'`, assumed to be a file object, and publishes `'header'` to the outport named `'port'`. If `'n'` is -1, the API creates a parallel stream connection and transfers data through it.

Output is possible only after the operator initializes; during prestart, timer, and port callbacks.

**Arguments**


<table>
<tr>
<td valign="top">

`data (...)`

</td>
<td valign="top">

The file object, such as `io.BytesIO`.

</td>
</tr>
<tr>
<td valign="top">

`n (int)`

</td>
<td valign="top">

The number of bytes to send.

If you set `n` to -1, the operator sends all bytes through a different stream connection. SAP doesn't recommend setting `n` to -1 for small binary chunks because it can create an overhead.

</td>
</tr>
<tr>
<td valign="top">

`header (Header|dict, optional)`

</td>
<td valign="top">

The dictionary mapping 'header name'-\>\['header content'\]. You can also use 'header' type from port callbacks. If you don't provide a header, the operator uses an empty header as default.

</td>
</tr>
<tr>
<td valign="top">

`response_callback(func[msg_id, ex], optional)`

</td>
<td valign="top">

The callback that's called after the next operator receives and processes the message correctly:

-   `'msg_id'` identifies the message and matches the return from the publish functions.
-   'ex' is an exception when there's one or 'none'. 'ex' comes from the message processing of the next operator. If there's no `response_callback`, the default function raises an exception if the value of 'ex' is None.



</td>
</tr>
</table>

**Returns**

`msg_id (bytes)`: 12-byte message unique identifier in a port-specific connection.

> ### Example:  
> ```
> # For this example, you need to create an input and output port
> # of type 'scalar' and type-id 'com.sap.core.binary'.
> 
> def on_input(msg_id, header, body):
> 
>     # Read body value when stream
>     body_reader = body.get_reader()
>     value = body_reader.read(-1)
>  
>     # Send first 5 bytes of value, if there is less, all data is 
>     # sent.
>     msg_id = api.outputs.output.publish(BytesIO(value), 5)
> 
>     body = b'foo bar baz'
>     # It is also possible to send at once, but it expects a file object
>     # In this case we use BytesIO
>     msg_id = api.outputs.output.publish(BytesIO(body), -1)
> 
> api.set_port_callback("input", on_input)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_uzv_f5k_lpb"/>

## api.outputs.port.with\_writer\(header=None, response\_callback=None\)

This API creates a stream writer to the outport named 'port'.

For dynamic ports, call `api.outputs.port.set_dynamic_type` before `api.outputs.port.with_writer`. For more details about dynamic ports, see the [Working With Dynamic Types](python3-operator-v2-1b5cca1.md#loio1b5cca1e8f3f418593d042661cc135ad__section_ll5_mhf_qqb) section.

Output is possible only after the operator initializes; during prestart, timer, and port callbacks.

**Arguments**


<table>
<tr>
<td valign="top">

`header (Header|dict, optional)`

</td>
<td valign="top">

The dictionary mapping 'header name'-\>\['header content'\]. You can also use 'header' type from port callbacks. If you don't provide a header, the operator uses an empty header as default.

</td>
</tr>
<tr>
<td valign="top">

`response_callback(func[msg_id, ex], optional)`

</td>
<td valign="top">

The callback that the operator calls after the next operator receives and processes the message correctly.

-   `'msg_id'` identifies the message and matches the return from the publish functions.
-   `'ex'` is an exception when there's one or 'none'. 'ex' comes from the message processing of the next operator. If there's no `response_callback`, the default function raises an exception if the value of 'ex' is None.



</td>
</tr>
</table>

**Returns**

-   `msg_id (bytes)`: 12-byte message unique identifier in a port-specific connection.
-   `writer (TableWriter|BinaryWriter)`: object with a stream connection open to the next operator.

> ### Example:  
> ```
> # For this example, you need to create an input and output port
> # of type 'scalar' and type-id 'com.sap.core.binary'.
> 
> def on_input(msg_id, header, body):
> 
>     # Read body value when stream
>     body_reader = body.get_reader()
>     value = body_reader.read(-1)
>  
>     try:
>         # Create stream writer
>         msg_id, writer = api.outputs.output.with_writer()
>         
>         # write input to output
>         writer.write(value)
>         
>         # write other binary to output
>         body = b'foo bar baz'
>         writer.write(body)
>     finally:
>         # Signals end of message and closes the connection even in case of Exceptions
>         writer.close()
> 
>     # It is also possible to send at once, either as a binary or file-object
>     # In this case we use BytesIO
>     msg_id = api.outputs.output.publish(BytesIO(body), -1)
> 
> api.set_port_callback("input", on_input)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_hcg_jwl_qrb"/>

## api.outputs.port.publish\(None, header=headers, response\_callback=None\)

This API publishes the type 'none' to outport named 'port'. The type 'none' contains only headers and no body data.

Output is possible only after the operator initializes; during prestart, timer, and port callbacks.

Arguments


<table>
<tr>
<td valign="top">

`None`

</td>
<td valign="top">

Signals the empty body because the 'none' type doesn't have data.

</td>
</tr>
<tr>
<td valign="top">

`header (Header|dict)`

</td>
<td valign="top">

The dictionary mapping 'header name'-\>\['header content'\]. You can also use 'header' type from port callbacks. If you don't provide a header, the operator uses an empty header as default.

</td>
</tr>
<tr>
<td valign="top">

`response_callback(func[msg_id, ex], optional)`

</td>
<td valign="top">

The callback that the operator calls after the next operator receives and processes the message correctly:

-   `'msg_id'` identifies the message and matches the return from the publish functions.
-   `'ex'` is an exception when there's one or 'none'. `'ex'` comes from the message processing of the next operator. If there's no `response_callback`, the default function raises an exception if 'ex' is None.



</td>
</tr>
</table>

**Returns**

`msg_id (bytes)`: 12-byte message unique identifier in a port-specific connection.

> ### Example:  
> ```
> # For this example, you need to create an input and output port
> # of arbitrary type. The body's content will not be consumed.
> import datetime
> 
> def on_input(msg_id, header, body):
> 
>     # Access single headers as dictionary and check if they are present
>     # to avoid errors
>     if 'header.type.id' in header:
>         header_val = header['header.type.id']
> 
>     # Header can be directly sent to the next operator, copy (.copy()) is also possible
>     api.outputs.output.publish(None, header)
> 
>     # New Headers can be a list or api.Record of the header's structure fields
>     new_header = api.Record([
>         "dummyConnection", # connection
>         "dummy/Path", # path
>         0, # size
>         False, #isDir
>         datetime.datetime.now().isoformat() # modTime
>     ])
> 
>     # For the output you need to create as specified a dict of single headers
>     # key: type-id of the single header
>     # value: list / api.Record of the header's structure fields
>     new_out_headers = {"com.sap.headers.file": new_header}
> 
>     # Also possible to send new header
>     api.outputs.output.publish(None, new_out_headers, None)
> 
> api.set_port_callback("input", on_input)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_bhb_pbf_qqb"/>

## api.outputs.port.set\_dynamic\_type\(dynamic\_type\)

This API associates the dynamic\_type received to the publisher. Call this API before 'with\_writer' when you use a dynamic port. If you type the port statically, the API issues an exception.

**Arguments**


<table>
<tr>
<td valign="top">

`dynamic_type (api.DataTypeReference)`

</td>
<td valign="top">

The dynamic type to associate with the current publisher.

</td>
</tr>
</table>

**Returns:** none.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_xxl_pty_1gb"/>

## Port Callbacks



### api.set\_port\_callback\(port, callback\)

This API associate input 'port' to the 'callback'. The operator calls 'callback' only when there's a message available in 'port'.

**Arguments**


<table>
<tr>
<td valign="top">

`port (str)`

</td>
<td valign="top">

The input port to associate with the callback.

</td>
</tr>
<tr>
<td valign="top">

`callback (func[msg_id, header, body])`

</td>
<td valign="top">

The callback that the operator calls for each new message sent to 'port'.

`'msg_id'` identifies the message. For information about 'header' and 'body', see the [Data Types](python3-operator-v2-1b5cca1.md#loio1b5cca1e8f3f418593d042661cc135ad__section_bgq_z25_zdb) section.

</td>
</tr>
</table>



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_c4y_ncf_qqb"/>

## Prestart



### api.set\_prestart\(callback\)

This API sets a 'callback' function to be executed before the event processing loop starts.

**Arguments**


<table>
<tr>
<td valign="top">

`callback (func[None])`

</td>
<td valign="top">

The callback that the operator executes before it executes any port and timer callbacks.

</td>
</tr>
</table>

> ### Example:  
> The following code snippet produces values 0,1,2 on the output port "output".
> 
> ```
> # For this example, you need to create an input port of type 'scalar'
> # and type-id 'com.sap.core.int64'
> 
> counter = 0
> 
> # The same as the default response callback
> def response_callback(msg_id, ex):
>     if ex:
>         raise ex
> 
> def prestart_function():
>     global counter
>     for i in range(0, 3):
>         api.outputs.output.publish(counter, response_callback=response_callback)
>         counter += 1
> 
> api.set_prestart(prestart_function)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_brx_5cf_qqb"/>

## Timers



### api.add\_timer\(callback\)

For this API, you can add multiple distinct periodic callbacks. Timers aren't preemptive, therefore, a set interval provides only the lower bound of the interval at which the API calls the timer function.

**Arguments**


<table>
<tr>
<td valign="top">

callback \(func\[None\]-\>float\)

</td>
<td valign="top">

The callback function to call. The call interval is the return in 'seconds'. If the return is '0', the API calls the next callback as fast as possible. If the return is a negative value, the timer stops.

</td>
</tr>
</table>

> ### Example:  
> The following code snippet produces value 0,1,2... on port "output" every 0,1,2... seconds until graph shutdown.
> 
> ```
> # For this example, you need to create an input port of type 'scalar'
> # and type-id 'com.sap.core.int64'
> 
> counter = 0
> 
> def t1():
>     global counter
>     api.outputs.output.publish(counter, {})
>     counter += 1
>     return counter
> 
> # The same as the default response callback
> def response_callback(msg_id, ex):
>     if ex:
>         raise ex
> 
> api.set_response_callback("output", response_callback)
> 
> api.add_timer(t1)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_qfn_1df_qqb"/>

## Shutdown



### api.set\_shutdown\(callback\)

This API sets a 'callback' function to execute after the operator's stop event.

**Arguments**


<table>
<tr>
<td valign="top">

callback \(func\[None\]\)

</td>
<td valign="top">

The callback executed after stopping the operator.

</td>
</tr>
</table>

> ### Example:  
> ```
> # For this example, you need to create an input port of arbitrary type
> counter = 0
> 
> def on_input(msg_id, header, body):
>     global counter
>     counter += 1
> 
> api.set_port_callback("input", on_input)
> 
> # The shutdown function will be called when the operator receives a stop signal
> # In this example it prints a simple information in the trace logs with the current message counter
> # You can check the graph diagnostics / traces of the graph for the shutdown message when the graph has stopped.
> def shutdown():
>     api.logger.info("shutdown: %d" % counter)
> 
> api.set_shutdown(shutdown)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_yxb_g25_zdb"/>

## Configuration API

The configuration API objects read configurations defined in either of the following ways:

-   Defined on the editor view of the operator.
-   Added in the configurations pane of the graph editor.

> ### Example:  
> If you define a configuration named "foo", access the configuration by calling `api.config.foo`.

The configuration APIs don't allow spaces in configuration field names. The "script" and "codelanguage" configuration fields don't appear in `api.config` because they are required configuration parameters. Therefore, don't use them. If you filled a configuration field with a JSON object in the Modeler, its value becomes a dictionary in Python.

> ### Note:  
> This API doesn't support additional configurations in the *Configuration* pane in the Modeler. However, you can still include configurations directly in the graph JSON, similar to `errorHandling` and `codelanguage`.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_utv_j25_zdb"/>

## Logging

To log messages, use the following APIs:

-   `api.logger.info("some text")`
-   `api.logger.debug("some text")`
-   `api.logger.warn("some text")`
-   `api.logger.error("some text")`



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_jtg_rdf_qqb"/>

## App Logging

Each call to the app logging functions results in an HTTP request, which can affect performance. The following are app logging APIs:

-   `api.app_log_error(message_code, message, details)`
-   `api.app_log_info(message_code, message, details)`
-   `api.app_log_warning(message_code, message, details)`

**Arguments**

The following table defines the arguments for the app logging APIs.


<table>
<tr>
<td valign="top">

`message_code (str)`

</td>
<td valign="top">

A response code, such as 200, 404, FA1001.

</td>
</tr>
<tr>
<td valign="top">

`message (str)`

</td>
<td valign="top">

The main log message.

</td>
</tr>
<tr>
<td valign="top">

`details (str)`

</td>
<td valign="top">

Additional information about the event to log.

</td>
</tr>
</table>



### api.app\_log\_error\(message\_code, message, details\)

This API logs errors into process logs.



### api.app\_log\_info\(message\_code, message, details\)

This API logs messages using the severity level 'info'.



### api.app\_log\_warning\(message\_code, message, details\)

This API logs messages using the severity level 'warning'.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_a1z_m25_zdb"/>

## Error Handling

Out of the four error handling options, only `propagate to error port` requires further support in the operator script. The `propagate to error port` option triggers messages to the `error` port using the error message format.

The operator allows customization of `code`, `text`, and `details` by raising `api.OperatorException`. If you don't use this exception type, the `com.sap.error` message has the following default values:

-   `code` as `0`
-   `text` as `exception message`
-   Empty `details`



### api.OperatorException\(code, text, details\)

This API is an exception to customize the `com.sap.error` message when you use the `propagate to error port` method.

**Arguments**


<table>
<tr>
<td valign="top">

`code (int)`

</td>
<td valign="top">

The error code that is specific to the operator.

</td>
</tr>
<tr>
<td valign="top">

`text (str)`

</td>
<td valign="top">

The string that corresponds to the main error message.

</td>
</tr>
<tr>
<td valign="top">

`details (api.Table)`

</td>
<td valign="top">

A table with the columns 'key' and 'value'. The columns are strings.

</td>
</tr>
</table>

> ### Example:  
> ```
> # For this example, you need to create an input port of arbitrary type 
> # and send a non-stream message to the input port to raise an exception.
> 
> # Instead of raising an exception like the default, this custom only logs
> # This function is called for all messages, but ex will contain an exception only if 'retry' is set.
> def custom_response_callback(msg_id, ex):
>     if ex:
>         api.logger.error("Error when publishing %s: %s" % (str(msg_id), str(ex)))
> 
> def on_input(msg_id, header, body):
>     try:
>         # Read body value when not stream
>         body_val = body.get()
>     except Exception as e:
>         code = 1
>         text = str(e)
>         # A 'com.sap.errors.details' table contains a list of key-value pairs
>         details = api.Table([['key', 'value']])
>         # If 'error_handling' is set to 'propagate to error port' the OperatorException will set the fields in the 'com.sap.error' message. 
>         raise api.OperatorException(code, text, details)
> 
> api.set_port_callback("input", on_input)
> ```

It's possible to raise any exception inside the script and have it treated according to the `error handling` configuration.

To configure the exception to stop the operator, use `api.propagate_exception(e)` in the script, where `e` is the exception.

> ### Note:  
> If the operator throws the exception inside a thread that's different than the script's main thread \(the main thread is the one running the callbacks\), the `api.propagate_exception(e)` configuration doesn't work. As a result, the script must rely on using `api.propagate_exception(e)` or sending the exception to the main thread.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_umj_1ft_fhb"/>

## Halting Execution

To halt the graph's execution with an error, follow the instructions in the [Error Handling](python3-operator-v2-1b5cca1.md#loio1b5cca1e8f3f418593d042661cc135ad__section_a1z_m25_zdb) section. To stop the graph without an error, configure the Python operator to send a signal to a Graph Terminator operator. For more information about the Graph Terminator, see [Graph Terminator V2](graph-terminator-v2-190cbc7.md).

Don't use the following Python commands:

-   Don't use `sys.exit(code)` because it causes only the current Python thread to exit.
-   Don't use `os._exit(code)` because it causes the whole Python process to quit and the entire graph to stop with an error.

To stop the whole graph with an error, follow the instructions in the [Error Handling](python3-operator-v2-1b5cca1.md#loio1b5cca1e8f3f418593d042661cc135ad__section_a1z_m25_zdb) section.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_fd5_525_zdb"/>

## repo\_root and subengine\_root

Access the `repo_root` and `subengine_root` path using the following APIs:

-   `api.repo_root`
-   `api.subengine_root`

SAP doesn't support accessing any file or folder under the path `/vrep`.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_vl4_qky_jgb"/>

## graph\_name, graph\_handle, and group\_id

Access the `graph_name`, `graph_handle`, and `group_id` values using the following APIs:

-   `api.graph_name`
-   `api.graph_handle`
-   `api.group_id`

The following table describes the values.


<table>
<tr>
<td valign="top">

`graph_name`

</td>
<td valign="top">

An identifier of a saved graph, such as `com.sap.dataGenerator`.

</td>
</tr>
<tr>
<td valign="top">

`graph_handle`

</td>
<td valign="top">

A unique identifier of the graph instance, referred to as “runtime handle” in the Modeler.

</td>
</tr>
<tr>
<td valign="top">

`group_id`

</td>
<td valign="top">

A unique identifier of the group where the operator is running.

</td>
</tr>
</table>



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_djx_fmp_23b"/>

## multiplicity, multiplicity\_index

Access `multiplicity` and `multiplicity_index` using the following APIs:

-   `api.multiplicity`
-   `api.multiplicity_index`

The following table describes the values.


<table>
<tr>
<td valign="top">

`multiplicity`

</td>
<td valign="top">

The multiplicity of the operator's group.

</td>
</tr>
<tr>
<td valign="top">

`multiplicity_index`

</td>
<td valign="top">

An integer in the range \[0, multiplicity\) that you can use to distinguish the multiple instances of this operator.

</td>
</tr>
</table>



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_inports_and_outports"/>

## Inports and Outports

To obtain the name of the inport and outport ports for the current operator instance, call the methods `api.get_inport_names()` and `api.get_outport_names()`, respectively.

To check which inports or outports are connected, call the `api.is_inport_connected` and `api.is_outport_connected` dictionaries. These dictionaries have the name of the port as key, and a boolean indicating whether the port is connected as value.

> ### Example:  
> ```
> if api.is_outport_connected["outport1"]:
>     r = do_some_expensive_calculation()
>     api.outputs.output1.publish({}, r)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_bgq_z25_zdb"/>

## Data Types

The SAP Data Intelligence Modeler specifies a data type by its type and its ID. A data type ID belongs to one of the following categories:

-   `scalar`: The most basic type of the Modeler's typing system. Scalar types are based on templates, which are a fixed set of type definitions.

-   `structure`: A named and ordered collection of fields. Each field is of type scalar or table. This collection of data is called a record.

-   `table`: A collection of many records or an ordered list of records. Table records contain only fields of type scalar.


Create new data types in the Modeler in the *Data Types* configuration section. Currently, you can create only structures and tables.

The following table contains the relationship between the core scalars, the type templates, and the Python type.


<table>
<tr>
<th valign="top">

Core Scalar

</th>
<th valign="top">

Type Template

</th>
<th valign="top">

Python Type

</th>
<th valign="top">

Observation

</th>
</tr>
<tr>
<td valign="top">

com.sap.core.binary

</td>
<td valign="top">

binary

</td>
<td valign="top">

bytes

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.bool

</td>
<td valign="top">

bool

</td>
<td valign="top">

bool

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.byte

</td>
<td valign="top">

uint8

</td>
<td valign="top">

int

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.date

</td>
<td valign="top">

date

</td>
<td valign="top">

datetime.date

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.decfloat16

</td>
<td valign="top">

decfloat16

</td>
<td valign="top">

decimal.Decimal

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.decfloat16

</td>
<td valign="top">

decfloat16

</td>
<td valign="top">

decimal.Decimal

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.float32

</td>
<td valign="top">

float32

</td>
<td valign="top">

float

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.float64

</td>
<td valign="top">

float64

</td>
<td valign="top">

float

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.geometry

</td>
<td valign="top">

geometry

</td>
<td valign="top">

bytes

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.geometryewkb

</td>
<td valign="top">

geometrywkb

</td>
<td valign="top">

bytes

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.int16

</td>
<td valign="top">

int32

</td>
<td valign="top">

int

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.int32

</td>
<td valign="top">

int64

</td>
<td valign="top">

int

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.int64

</td>
<td valign="top">

int64

</td>
<td valign="top">

int

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.int8

</td>
<td valign="top">

int8

</td>
<td valign="top">

int

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.string

</td>
<td valign="top">

string

</td>
<td valign="top">

str

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.time

</td>
<td valign="top">

time

</td>
<td valign="top">

datetime.time

</td>
<td valign="top">

Loss of precision. Can only represent up to microseconds.

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.timestamp

</td>
<td valign="top">

timestamp

</td>
<td valign="top">

datetime.datetime

</td>
<td valign="top">

Loss of precision. Can only represent up to microseconds.

</td>
</tr>
<tr>
<td valign="top">

com.sap.core.uint8

</td>
<td valign="top">

uint8

</td>
<td valign="top">

int

</td>
<td valign="top">

N/A

</td>
</tr>
</table>

The Modeler represents the following templates as a `string`:

-   `decimal`
-   `date`
-   `time`
-   `timestamp`

When you retrieve one of the templates, SAP converts the object to a high-level class for easier manipulation. Retrieve the raw string representation of the object by calling `.get_raw()`.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_elc_dhf_qqb"/>

## Data Type Reference



### api.DataTypeReference\(type, ID\)

Use this API to refer to data types.

**Arguments**


<table>
<tr>
<td valign="top">

`type (str)`

</td>
<td valign="top">

Identifies the type as "scalar", "structure" or "table".

</td>
</tr>
<tr>
<td valign="top">

`ID (str)`

</td>
<td valign="top">

The ID from type.

</td>
</tr>
</table>

Access the type and ID of a `DataTypeReference` object using the `.type_` and `.type_id` attributes respectively.

> ### Example:  
> ```
> int64_type = api.DataTypeReference("scalar", "com.sap.core.int64")
> 
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_kmv_hhf_qqb"/>

## Type Context

The type context provides access to methods that interact with the type system, such as checking if a type exists or creating a new dynamic type. Access the type context as an attribute of `api.type_context`. The `api.type_context` attribute offers several methods to interact with the type system for data types:

-   `api.type_context.create_new_table(columns, keys=None)`
-   `api.type_context.register_schema(schema, scope)`
-   `api.type_context.infer_schema_from_row(row, colnames=None)`
-   `api.type_context.get_vtype(reference)`



### api.type\_context.create\_new\_table\(columns, keys=None\)

This method creates a new dynamic table containing the specified columns. For an example, see [Working With Dynamic Types](python3-operator-v2-1b5cca1.md#loio1b5cca1e8f3f418593d042661cc135ad__section_ll5_mhf_qqb).

**Arguments**


<table>
<tr>
<td valign="top">

`columns (dic[str|api.DataTypeReference])`

</td>
<td valign="top">

A dictionary that maps column names to their types.

</td>
</tr>
<tr>
<td valign="top">

`keys (List[str], optional)`

</td>
<td valign="top">

A list of the key columns names.

</td>
</tr>
</table>

**Returns**

`ref (api.DataTypeReference)`: reference to the created type.



### api.type\_context.register\_schema\(schema, scope\)

This method registers a new data type definition to use in the graph. The schema is the JSON object definition for the data type. The API expects values for at least the keys `name` and `vflow.type`.

You must provide a scope for the lookup of the data type name, which is updated to the schema definition internally.

For registering structure and table data types, provide an optional graph ID to associate the schemas to the graph as graph-local types.

**Arguments**


<table>
<tr>
<td valign="top">

`schema (Dict[str, Any])`

</td>
<td valign="top">

A Python dictionary that contains the object definition of a data type.

</td>
</tr>
<tr>
<td valign="top">

`scope (str)`

</td>
<td valign="top">

The scope in which the data type is used. Options are as follows:

-   'dynamic'
-   'local'
-   'inline'



</td>
</tr>
</table>

**Returns**

`str`: given name of the data type to be registered.



### api.type\_context.infer\_schema\_from\_row\(row, colnames=None\)

Infers the JSON object schema definition that the method returns as a Python dictionary from a row in the table. This method is applicable for the table data types only. The method iterates over the values and tries to infer the data type to construct a data type table definition. It has \['vflow.type'\] as 'table', and a list of scalar data type definitions embedded inside the key hierarchy `['row']['components']`.

Optionally, you can provide column names as an argument. Set the length of the `row` and `colnames` arguments to the same size, if possible. When you provide column names, schema definition dictionary objects use the column names as keys along with their respective scalar data type definition as values. If you don't provide column names, the operator infers column names as `'col<index>'`. For example, col0, col1, col2. If a row has a greater length compared to the `colnames` argument, then the API uses `'col<index>'` when it exhausts the names in `colnames`.

**Arguments**


<table>
<tr>
<td valign="top">

`row (Iterable[Any])`

</td>
<td valign="top">

The values to infer.

</td>
</tr>
<tr>
<td valign="top">

`colnames (Iterable[str], optional)`

</td>
<td valign="top">

The column names to use in the inferred schema.

</td>
</tr>
</table>

**Returns**

`Dict[str, Any]`: Python dictionary object with the table vType schema definition.



### api.type\_context.get\_vtype\(reference\)

Returns a data type definition from the provided reference. The reference is an instance of the `api.DataTypeReference` class, and it carries the following key information:

-   Base type of the data type \(scalar, structure, table, or none\).
-   Type-id

Depending on the base type, the `api.type_context.get_vtype(reference)` method returns one of the concrete data type class instances that describe the type itself.

**Arguments**


<table>
<tr>
<td valign="top">

`reference (api.DataTypeReference)`

</td>
<td valign="top">

An object of the `api.DataTypeReference` class.

</td>
</tr>
</table>

**Returns**

`Union[VTypeScalar, VTypeStructure, VTypeTable, VTypeNone]`: One of the concrete vType class instances. vType class instances are essentially `api.DataTypeReference` objects with corresponding types: scalar, structure, table, and none.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_hmz_sxy_qsb"/>

## VTypes Attributes

VType attributes retrieve a concrete vType class object using the method `api.type_context.get_vtype` and the type reference `api.DataTypeReference`. With these methods, access more details about the specific type. The following table contains descriptions for the attributes that are available for all VTypes.


<table>
<tr>
<th valign="top">

Attribute

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`vType.scope (str)`

</td>
<td valign="top">

The scope in which you can use the data type. Options are as follows:

-   'global'
-   'dynamic'
-   'local'
-   'inline'



</td>
</tr>
<tr>
<td valign="top">

`vtype.name (str)`

</td>
<td valign="top">

The name of the data type, usually the type ID.

</td>
</tr>
<tr>
<td valign="top">

`vtype.description (str)`

</td>
<td valign="top">

A description of the VType.

</td>
</tr>
</table>

**Additional VType attributes**

Each specific VType class has additional attributes.



### VTypeScalar

The scalar VType class contains the attributes described in the following table.


<table>
<tr>
<th valign="top">

Attribute

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`vTypeScalar.template (str)`

</td>
<td valign="top">

The template of the scalar vType.

</td>
</tr>
<tr>
<td valign="top">

`vTypeScalardinamically(int)`

</td>
<td valign="top">

The type precision for vTypes that have the decimal template.

</td>
</tr>
<tr>
<td valign="top">

`vTypeScalar.scale (int)`

</td>
<td valign="top">

The type scale for vTypes that have the decimal template.

</td>
</tr>
<tr>
<td valign="top">

`vTypeScalar.length (int)`

</td>
<td valign="top">

The type length for string or binary values.

</td>
</tr>
</table>



### VTypeStructure

The structure vType class contains the attribute in the following table.


<table>
<tr>
<th valign="top">

Attribute

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`vTypeStructure.fields (Dict[str, api.DataTypeReference])`

</td>
<td valign="top">

The dictionary that maps the structure field names to their types.

</td>
</tr>
</table>



### VTypeTable

The table vType class contains the attributes in the following table.


<table>
<tr>
<th valign="top">

Attribute

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`vTypeTable.columns (Dict[str, api.DataTypeReference])`

</td>
<td valign="top">

The dictionary mapping the column names to their types.

</td>
</tr>
<tr>
<td valign="top">

`vTypeTable.keys (List[str])`

</td>
<td valign="top">

A list of the key column names.

</td>
</tr>
</table>

> ### Example:  
> The following code snippet gets the column names of a table:
> 
> ```
> # For this example, you need to create an input port of 'table' type.
> 
> def on_input(msg_id, header, body):
>     table = body.get()
>     table_def = api.type_context.get_vtype(table.get_type_reference())
>     column_names = list(table_def.columns.keys())
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_ll5_mhf_qqb"/>

## Working with Dynamic Types

Ports can be either static or typed dynamically as follows:

-   Static ports have a fixed type and ID.
-   Dynamic ports keep the fixed type, but allow for any type ID to be sent or received. For example, a dynamic table output that always outputs tables, but each table has a different schema.

The ID of a dynamic port is `*`.

When you use dynamic ports to output data through streams with the `with_writer` interface, call `publisher.set_dynamic_type` to associate a type to the dynamic port. If the data doesn't contain the type information when you use the `publish` interface, the engine tries to infer the type information.

> ### Example:  
> The following code snippet creates a new table in runtime and associates the table to a publisher before getting the writer:
> 
> ```
> # For this example, you need to create an output port called 
> # 'myDynamicPort' of 'table' type and type-id '*'.
> 
> def create_new_dynamic_table():    
>     columns_definition = {
>       "id": api.DataTypeReference("scalar", "com.sap.core.int64"),
>       "name": api.DataTypeReference("scalar", "com.sap.core.string"),
>       "mean": api.DataTypeReference("scalar", "com.sap.core.float64")
>     }
>     table_type_ref = api.type_context.create_new_table(
>         columns = columns_definition,
>         keys = ["id"])
>     
>     api.outputs.myDynamicPort.set_dynamic_type(table_type_ref)
>     
>     try:
>         _, writer = api.outputs.myDynamicPort.with_writer()
> 
>         data = [
>             [1, "Lorem ipsum", 5.3],
>             [2, "dolor sit", 6.2],
>             [3, "amet consectetur", 7.2]
>         ]
> 
>         table = api.Table(data)
>         
>         while len(table) > 0:
>             # Write up to 100 records at once
>             writer.write(table[:100])
>             # Remove these records from the table
>             table = table[100:]
>     finally:
>         # Close writer stream when done processing the full table
>         writer.close()
>     
> api.set_prestart(create_dynamic_table)
> ```

> ### Example:  
> In the following code snippet, the engine infers the columns instead of defining them manually:
> 
> ```
> # For this example, you need to create an output port called 
> # 'myDynamicPort' of 'table' type and type-id '*'.
> 
> def create_dynamic_table():
>     
>     data = [
>         [1, "Lorem ipsum"],
>         [2, "dolor sit"],
>         [3, "amet consectetur"]
>     ]
>         
>     table = api.Table(data, infer_type=True)
>     
>     api.outputs.myDynamicPort.set_dynamic_type(table.get_type_reference())
>     
>     msg_id, w = api.outputs.myDynamicPort.with_writer()
>     w.write(table)
>     w.close()
>     
> api.set_prestart(create_dynamic_table)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_p15_5hf_qqb"/>

## Record

A Record is an iterable class that represents a collection of either scalars or tables. Call the record's constructor from `api.Record`. Access the record's elements through indexing.



### api.Record\(values\)

**Arguments**


<table>
<tr>
<td valign="top">

`values (list)`

</td>
<td valign="top">

The data to compose the record's fields.

</td>
</tr>
</table>

**Returns**

`new_record (api.Record)`: created `api.Record`.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_h5r_l3f_qqb"/>

## Table

A Table is an iterable class that represents an ordered collection of rows. Call a table's constructor from `api.Table`. Access a table's elements through indexing.

Tables can have an associated type or not. A typed table is a table that has an associated type. Create a typed table in one of the following ways:

-   Pass the applicable type on its constructor.
-   Instantiate a new table with `infer_type=True`.
-   Call `infer_dynamic_type` to create a new dynamic type to represent it.

Even though there are ways to convert tables to dataframes and dataframes to tables, the conversion affects performance. Therefore, try to avoid transforming dataframes and tables.



### api.Table\(data, type\_id="", infer\_type=False, colnames=None\)

**Arguments**


<table>
<tr>
<td valign="top">

`data (List[List[Any]])`

</td>
<td valign="top">

The data to compose the table body. Enter as a list of rows \(list of lists\).

</td>
</tr>
<tr>
<td valign="top">

`type_id (str)`

</td>
<td valign="top">

The ID of type to associate to the table.

</td>
</tr>
<tr>
<td valign="top">

`infer_type (bool)`

</td>
<td valign="top">

When type ID isn't provided, determines whether to infer and set the table type.

</td>
</tr>
<tr>
<td valign="top">

`colnames (List[str], optional)`

</td>
<td valign="top">

When `infer_type=True`, specifies the names of the table columns to use in the inferred type.

If names aren't provided, the names are `"col<index>"`, where `"<index>"` is the column index. For example, col0, col1, col2.

If the number of table columns is greater than the `colnames` size, and names in `colnames` are exhausted, the API uses `'col<index>'`.

</td>
</tr>
</table>

Returns

`new_table (api.Table)`: created `api.Table`.

Tables offer the following methods:

-   `table.is_typed()`
-   `table.get_type_reference()`
-   `table.infer_dynamic_type(colnames=None)`
-   `table.to_dataframe()`
-   `api.Table.from_dataframe(df, vtype_id="", infer_type=False)`



### table.is\_typed\(\)

**Returns**

`(bool)`: boolean specifying whether the table has an associated type.



### table.get\_type\_reference\(\)

**Returns**

`(api.DataTypeReference)`: reference to type associated to table. If table isn't typed, returns None.



### table.infer\_dynamic\_type\(colnames=None\)

This method creates a new dynamic type to represent the table schema. The column types are inferred based on the inner data. After the table is called, the table is typed.

**Arguments**


<table>
<tr>
<td valign="top">

`colnames (List[str], optional)`

</td>
<td valign="top">

The table column names to use in the created type. If you don't provide the names, the names are 'col*<index\>*', where “*<index\>*” is the column index. For example, col0, col1, and so on.

If the number of table columns is greater than colnames size, the method uses 'col*<index\>*' when names in colnames are exhausted.

</td>
</tr>
</table>

**Returns**

`type_ref (api.DataTypeReference)`: a reference to new inferred type.



### table.to\_dataframe\(\)

**Returns**

-   `new_df (pandas.DataFrame)`: the dataframe created from the table.

    > ### Note:  
    > pandas is Python software library.

-   `headers (dict)`: the extracted headers from the table.

> ### Example:  
> ```
> def get_df(msg_id, header, body):
>     # Get an API Table from the body
>     table = body.get()
> 
>     # Transform the table into dataframe
>     df, _ = table.to_dataframe()
>     
> # Run every time an input is received
> api.set_port_callback("input", get_df)
> ```



### api.Table.from\_dataframe\(df, vtype\_id="", infer\_type=False\)

Creates a table from the given pandas \(Python software library\) dataframe. The table is indicated in the arguments.

**Arguments**


<table>
<tr>
<td valign="top">

`df (pandas.DataFrame)`

</td>
<td valign="top">

The dataframe that contains the data to convert.

</td>
</tr>
<tr>
<td valign="top">

`vtype_id (str)`

</td>
<td valign="top">

The ID of the associated table type.

</td>
</tr>
<tr>
<td valign="top">

`infer_type (bool)`

</td>
<td valign="top">

If `vtype_id` isn't provided, specifies whether to infer and set the table type. If `True`, the column names in the inferred type are the same as the names in the dataframe.

</td>
</tr>
</table>

Returns

`new_table (api.Table)`: the created `api.Table`.

> ### Example:  
> ```
> def create_table(msg_id, header, body):
>     # Get a dataframe from the body
>     df = body.get()
> 
>     # Transform the dataframe into table
>     table = api.Table.from_dataframe(df, "$GRAPH.tableExample")
>     
>     # Send to output via writer
>     _ , writer = api.outputs.output.with_writer()
>     writer.write(table)
>     writer.close()
>     
> # Run every time an input is received
> api.set_port_callback("input", create_table)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_hfs_djf_qqb"/>

## Header

A header is a read-only dictionary for which the first level is expected to have `str` as keys and `List` or `api.Record` as values.

Because the header is a read-only structure, modify it by calling the header's `.copy()` method for a `dict` representation of the received header. A `dict` representation prevents unexpected changes because operators can point to the same header.

> ### Example:  
> ```
> # For this example, you need to create an input and output port
> # of arbitrary type. But they need to be of the same type and type-id.
> import datetime
> 
> def on_input(msg_id, header, body):
>     # Access single headers as dictionary and check if they are present
>     # to avoid errors
>     if 'header.type.id' in header:
>         api.logger.info(header['header.type.id'])
> 
>     dic_header = header.copy()
>     # New Headers can be a list or api.Record of the header's structure fields
>     new_header = api.Record([
>         "dummyConnection", # connection
>         "dummy/Path", # path
>         0, # size
>         False, #isDir
>         datetime.datetime.now().isoformat() # modTime
>     ])
> 
>     # key: type-id of the single header
>     # value: list / api.Record of the header's structure fields
>     dic_header["com.sap.headers.file"] = new_header
>     
>     # sending the modified 'header' to the next operator
>     api.outputs.output(body, dic_header)
> 
>     # can also send the received header directly
>     api.outputs.output(body, header)
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_qdh_jjf_qqb"/>

## InputBody

The InputBody class wraps the incoming data. The callback receives InputBody with the message ID and the headers. Depending on the type of associated port, the InputBody gives access directly to the object received or to a stream.

InputBody offers the following functions:

-   `body.get()`
-   `body.get_reader()`
-   `body.is_stream()`
-   `body.get_type_id()`
-   `body.get_base_type*)`



### body.get\(\)

Returns the data object for the following types:

-   `(scalar, *)`: \* for any scalar except for the ones based on the "binary" template.
-   `(structure, *)`
    -   **Returns:** data, the type depends on the type and ID of the associated input port.

-   `(table, *)`
    -   **Returns:** `api.Table` with the complete table contents. `api.Table` reads the whole table. To avoid memory issues, consume the table in parts. For more information, read about the method `body.get_reader()`.

-   `(none)`
    -   **Returns:** none, because the 'none' type has no body.


> ### Note:  
> If the function calls `'get'` for an unsupported type, the API issues an exception.



### body.get\_reader\(\)

Reader, if the port type is of one of the following types:

-   `(scalar, *)`: \* for any scalar based on the "binary" template.
-   `(table, *)`

**Returns**

`(Reader|TableReader)`: stream reader.

> ### Note:  
> If the function calls 'get\_reader' for an unsupported type, such as a string, the API issues an exception.



### body.is\_stream\(\)

**Returns**

`(bool)`: flags whether the body supports streaming.



### body.get\_type\_id\(\)

**Returns**

`(string)`: the type ID of the associated port.



### body.get\_base\_type\(\)

This function returns the type of the associated data.

**Returns**

`(string)`: "scalar", "structure", "table" or "none".



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_tzb_gkf_qqb"/>

## TableWriter

This class designates objects to write into table streams. With tables, it's possible to output the table as a batch. For example, use the publish function of the publisher.

TableWriter offers the following functions:

-   `writer.write(rows)`
-   `writer.close()`



### writer.write\(rows\)

This function writes a list of rows into the stream.

**Arguments**


<table>
<tr>
<td valign="top">

`rows (List[List] | api.Table)`

</td>
<td valign="top">

The table object to stream.

</td>
</tr>
</table>

**Returns**

`n (int)`: the number of rows written successfully.



### writer.close\(\)

This function closes the stream connection. To guarantee closing the writers, SAP recommends using `'try-finally'` clauses. The `'try-finally'` clauses avoid hanging streams when there are unforeseen exceptions.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_uhf_mkf_qqb"/>

## TableReader

This class designates the objects from which the table stream reads. There's no EOF that signals if the writer closed the stream. Instead, there's an empty table.



### reader.read\(n=-1\)

This function reads a list of rows from the stream and returns the list in a table format. If less than the specified number of rows is available, and the stream is still open, the `reader.read(n=-1)` function is blocked from returning. If the stream is closed, read can return less than `n` rows. If you set `n` to `-1`, the function reads the rows until the TableWriter closes the stream.

**Arguments**


<table>
<tr>
<td valign="top">

`n (int)`

</td>
<td valign="top">

The number of rows to read.

</td>
</tr>
</table>

**Returns**

`table (api.Table)`: the table object that contains the read rows.

> ### Example:  
> ```
> # For this example, you need to create an input of 'table' type.
> 
> def on_input(msg_id, header, body):
>     table_reader = body.get_reader()
>     while True:
>         table = table_reader.read(5) # Read 5 rows of the table
>         # Do something with the table
>         if len(table) < 5: # This means the stream is over
>             break
> ```



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_y4g_vkf_qqb"/>

## BinaryWriter

This class controls the objects to write into Binary streams. BinaryWriter also outputs the bytes as a batch, such as by using the publish function.

The BinaryWriter class contains the following functions:

-   `writer.write(data)`
-   `writer.flush()`
-   `writer.close()`



### writer.write\(data\)

This function writes bytes into the stream.

**Arguments**


<table>
<tr>
<td valign="top">

`data (bytes)`

</td>
<td valign="top">

The bytes to stream.

</td>
</tr>
</table>

**Returns**

`n (int)`: the number of bytes written to the stream successfully.



### writer.flush\(\)

This function flushes the stream connection.



### writer.close\(\)

This function closes the stream connection.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_kjw_zkf_qqb"/>

## BinaryReader

this class designates the objects to read from a stream of bytes. The function indicates the end of the stream when it returns 0 bytes and the size wasn't 0.



### reader.read\(n=-1\)

This function read the set number of bytes from the stream. The system blocks the function from returning bytes when less than the set number of bytes is available and the stream is still open. If the stream is closed, the function can return less than n bytes. If you set bytes to -1, the function reads bytes until the writer closes the stream.

**Arguments**


<table>
<tr>
<td valign="top">

n \(int\)

</td>
<td valign="top">

The number of bytes to read.

</td>
</tr>
</table>

**Returns**

`data (bytes)`: the bytes that the function read.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_qm4_jf5_zdb"/>

## Correspondence Type Templates, Python Types, and dtypes

When the functions read a table as a dataframe, the Modeler converts the individual pieces of the data from the table to a different format.

The following table lists the expected dtype for an element of a scalar type after the conversion from the table format to a pandas dataframe.


<table>
<tr>
<th valign="top">

Type Template

</th>
<th valign="top">

Python Type

</th>
<th valign="top">

dtype

</th>
<th valign="top">

Limitations

</th>
</tr>
<tr>
<td valign="top">

bool

</td>
<td valign="top">

bool

</td>
<td valign="top">

bool

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

int8

</td>
<td valign="top">

int

</td>
<td valign="top">

int64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

int16

</td>
<td valign="top">

int

</td>
<td valign="top">

int64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

int32

</td>
<td valign="top">

int

</td>
<td valign="top">

int64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

int64

</td>
<td valign="top">

int

</td>
<td valign="top">

int64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

uint64

</td>
<td valign="top">

int

</td>
<td valign="top">

uint64\*

</td>
<td valign="top">

\*The smallest possible between uint8, uint16, uint32, and uint64 that can hold all values.

</td>
</tr>
<tr>
<td valign="top">

float32

</td>
<td valign="top">

float

</td>
<td valign="top">

float64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

float64

</td>
<td valign="top">

float

</td>
<td valign="top">

float64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

decimal

</td>
<td valign="top">

str

</td>
<td valign="top">

object\*

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

date

</td>
<td valign="top">

str

</td>
<td valign="top">

datetime64\[ns\]

</td>
<td valign="top">

Can represent only range: 1677-09-21 - 2262-04-11

</td>
</tr>
<tr>
<td valign="top">

time

</td>
<td valign="top">

str

</td>
<td valign="top">

datetime64\[ns\]

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

timestamp

</td>
<td valign="top">

str

</td>
<td valign="top">

datetime64\[ns\]

</td>
<td valign="top">

Can represent only range: 1677-09-21 00:12:43.145225 - 2262-04-11 23:47:16.854775807

</td>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">

str

</td>
<td valign="top">

object

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

geometry

</td>
<td valign="top">

bytes

</td>
<td valign="top">

object

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

geometryewkb

</td>
<td valign="top">

bytes

</td>
<td valign="top">

object

</td>
<td valign="top">

N/A

</td>
</tr>
</table>

When there are nulls, the corresponding value in a dataframe is of type pd.NA \(not available\). When nulls are present, the columns have mixed types and the column dtype is object.



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_typ_yfr_ywb"/>

## Snapshot

Use snapshot on operators that have an internal state, which we call “stateful”. Not all stateful operators require that you implement the snapshot functions. To declare the operator as stateful, it has to have the option set when calling `set_initial_snapshot_info`. If it has a state, the operator has to implement at least `set_restore_callback` and `set_serialize_callback`.

> ### Note:  
> The snapshot feature impacts the graph runtime, but provides you with the ability to recover the graph.

Operators that support snapshot can have two extra classes: generators and writers. Generators are further guarantees in [api.OutportInfo](python3-operator-v2-1b5cca1.md#loio1b5cca1e8f3f418593d042661cc135ad__section_qcn_mmw_ywb).

Writers are operators that have effects outside the graph, such as operators that write into databases, to a publisher, or to a subscriber queue. If an operator is a writer and it's stateful, it offers an at-least-once guarantee. At-least-once guarantees mean that there's a guarantee that data isn't lost, even though it can be written twice. Being stateful requires implementing the restore and serialize functions. It's also possible to have exactly-once guarantee, which requires the writer to be idempotent as well as stateful. Idempotency means equivalency when writing the same data several times.

For more information about the snapshot feature, see the *Modeling Guide*.

The following points are general observations about the snapshot functions and how operators can support snapshot:

-   A port callback can't be blocked while it waits for another port callback. This block leads to a deadlock.
-   Before saving a state, the operator can't pause the shutdown function, which prevents the shutdown function from changing the operator state.

> ### Example:  
> The following example scripts show the snapshot functions usage.
> 
> ```
> # This example will accumulate all the numeric values it gets on the input
> # and it will recover when the graph crashes with the accumulated value stored as state of this operator
> # When using the snippet below make sure you create input port of the type-id com.sap.core.int64 
> # and output port of the type-id com.sap.core.string.
> # You can use the prestart example as a generator operator for the integer inputs
> # Also make sure to start the graph with State Management enabled (via Run As..)
> 
> # State Management needs to be only implemented for operators which need to store a state 
> # that influences the processing of the input messages (like in this example adding the accumulated value to the output).
> # If you can process the input message independently of any state variable 
> # (For example, the output is always the same for the same input message after a graph recovery)
> # then you don't need to implement these methods as your operator is considered stateless.
> import pickle
> import random
> import time
> 
> # Internal operator state
> acc = 0
> 
> def on_input(msg_id, header, body):
>     global acc
>     v = body.get()
>     acc += v
>     if random.randint(1,101) % 100 == 0:
>         # Enforce a crash with 1% chance to enforce a recovery restart
>         # But sleep 10 seconds to ensure you view the results of the output
>         time.sleep(10)
>         raise Exception("crashed with 1% chance. Feel free to adjust the chance based on your needs.")
>     api.outputs.output.publish("%d: %d" % (v, acc))
> 
> api.set_port_callback("input", on_input)
> 
> # It is required to have 'is_stateful' set. 
> # But, since this operator script doesn't define a generator, 
> # no information about output port is passed.
> 
> api.set_initial_snapshot_info(api.InitialProcessInfo(is_stateful=True))
> 
> def serialize(epoch):
>     return pickle.dumps(acc)
> 
> api.set_serialize_callback(serialize)
> 
> def restore(epoch, state_bytes):
>     global acc
>     acc = pickle.loads(state_bytes)
> 
> api.set_restore_callback(restore)
> 
> def complete_callback(epoch):
>     api.logger.info(f"epoch {epoch} is completed!!!")
> 
> api.set_epoch_complete_callback(complete_callback)
> ```





### api.InitialProcessInfo

Class for initial snapshot information about the operator.

**Arguments**


<table>
<tr>
<td valign="top">

`is_stateful (bool, optional)`

</td>
<td valign="top">

Specifies whether the operator has an internal state to store. Default is false.

</td>
</tr>
<tr>
<td valign="top">

`outports_info (Dict[str, api.OutportInfo], optional)`

</td>
<td valign="top">

A dictionary that configures the output ports. The default is an empty dictionary.

</td>
</tr>
</table>





### api.OutportInfo

This function is the class for operator output port information.

**Arguments**


<table>
<tr>
<td valign="top">

`is_generator (bool, optional)`

</td>
<td valign="top">

Specifies whether the operator is a generator.

A generator is a port that produces outputs that are independent of input port data. All graphs that have data flowing have at least one generator output port.

Examples of generators include operators reading files with no input connected or Kafka consumers.

</td>
</tr>
</table>





### api.set\_initial\_snapshot\_info\(initial\_process\_info

This function sets the initial information for a snapshot before starting the operator. Call `api.set_initial_snapshot_info(initial_process_info)` outside of the callback functions.

**Arguments:** `initial_process_info (api.InitialProcessInfo)`





### api.set\_restore\_callback\(callback\)

This is a register function that restores the operator state.

**Arguments:**


<table>
<tr>
<td valign="top">

`callback (func[str, bytes] -> None])`

</td>
<td valign="top">

The function expects two input parameters as follows:

-   The first is the epoch, which uniquely identifies the state that is being recovered.
-   The second is the serialized operator state.



</td>
</tr>
</table>



api.set\_serialize\_callback\(callback\)

This is a register function that returns the operator state.

**Arguments**


<table>
<tr>
<td valign="top">

`callback (func[str] -> bytes)`

</td>
<td valign="top">

The function expects the epoch as a parameter. Epoch uniquely identifies the state that is being recovered. It returns the serialized operator state.

</td>
</tr>
</table>

Operators that support snapshot shouldn't spawn new threads or processes. Spawning new threads or processes can change the internal operator state or send data to the output ports. If you can't avoid this situation, use `set_pause_callback` and `set_resume_callback`.

> ### Example:  
> An operator starts a thread inside an input port callback and this thread writes into output ports. You implement the two functions that rely on `threading.Lock` as follows: :
> 
> -   The `set_pause_callback` function acquires the lock.
> -   The `set_resume_callback` function releases the lock.





### api.set\_pause\_callback\(None\)

This function finishes or pauses all actions that affect the internal operator state before it returns.





### api.set\_resume\_callback\(None\)

This function has to recover all actions that were stopped when pausing the operator.



### api.set\_epoch\_complete\_callback\(callback\)

**Arguments**

Call this function when all operators in a graph have saved their states, which is when the state identified by the epoch and sent as a parameter to this function is over.


<table>
<tr>
<td valign="top">

`callback (func[str] -> None)`

</td>
<td valign="top">

 

</td>
<td valign="top">

Specifies the epoch that is passed as a parameter.

</td>
</tr>
</table>



<a name="loio1b5cca1e8f3f418593d042661cc135ad__section_r3j_5pw_ywb"/>

## FAQ

**Where do I put initialization code for my operator?**

Execute the script once, but execute the callback functions defined in the script multiple times as necessary. Execute the commands from the script's outermost scope once, by placing the initialization code in the body of the script.

> ### Example:  
> The following code snippet illustrates the answer to the FAQ:
> 
> ```
> # Hypothetical script for Python3Operator
> 
> # In the operator's initialization we might want to setup a connection
> # with a database for example ('setup_connection' is an hypothetical function):
> db = setup_connection(api.config.host, api.config.port)
> 
> def my_callback_func(data):
>     global db
>     db.write(data)  # hypothetical call
> 
> api.set_port_callback("input", my_callback_func)
> ```

As an alternative, place the initialization code in the prestart function by registering a function with `api.set_prestart(func)`.

Output is possible only after the operator initializes; during prestart, timer, and port callbacks.

