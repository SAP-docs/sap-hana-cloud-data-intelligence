<!-- loio021180336add475bbd712b0ce5d393c1 -->

# Python3 Operator

Use the Generation 1 Python3 operator to define a script that offers convenience functions from API objects, such as callbacks.



> ### Example:  
> Set a callback function that the operator calls when it receives new data in the “datain” port by writing `api.set_port_callback("datain", callback_name)`.

> ### Note:  
> Each callback that you register in the script runs in a different thread. As the script developer, you handle potential concurrency issues such as race conditions. For example, use primitives from the Python threading module to protect against these concurrency issues. For more information about the Python threading module, see [threading module](https://docs.python.org/3/library/threading.html) in the Python documentation.

You can create an operator that extends the Python3 operator directly in the *Repository* tab of the Modeler application. For more information about extensions, see the [Operator Details](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/2a647f3e65454a1b9e0b66c393bed530.html "Every operator has an ID (also known as name) and a title (also known as the description). The operator ID is a unique identifier, with a strict format. The operator title is what the graphical interface displays.") :arrow_upper_right: topic in the *Modeling Guide*.

> ### Note:  
> The Python3 operator runs on Python 3.9, which was updated from Python 3.6. You don't have to change the APIs provided by the operator. The main incompatible change is the addition of “async” and “await” as reserved words and their use with the asyncio module. Find a complete list of new features at the following locations:
> 
> -   [https://docs.python.org/3/whatsnew/3.7.html](https://docs.python.org/3/whatsnew/3.7.html)
> 
> -   [https://docs.python.org/3/whatsnew/3.8.html](https://docs.python.org/3/whatsnew/3.8.html)
> 
> -   [https://docs.python.org/3/whatsnew/3.9.html](https://docs.python.org/3/whatsnew/3.9.html)
> 
> 
> Packages used by the Python3 operator can include breaking changes as follows:
> 
> -   **Tornado 5.0.2 to 6.1.0:** For the Tornado list of news, see [https://github.com/tornadoweb/tornado/blob/stable/docs/releases/v6.0.0.rst](https://github.com/tornadoweb/tornado/blob/stable/docs/releases/v6.0.0.rst). SAP Doesn't expect these changes to affect operators.
> -   **Pandas 1.0.3 to 1.2.5:** Pandas \(Python software library\) has no breaking changes, however, deprecated features generate a warning. For a list of deprecated features, see [https://pandas.pydata.org/pandas-docs/dev/whatsnew/v1.2.0.html](https://pandas.pydata.org/pandas-docs/dev/whatsnew/v1.2.0.html).
> 
> Be aware that some of the used packages with Python 3.6 require new versions to work with Python 3.9.



<a name="loio021180336add475bbd712b0ce5d393c1__section_sq1_nf3_vdb"/>

## Configuration Parameter

The following table describes the Python3 operator configuration parameter.


<table>
<tr>
<th valign="top">

Name

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

*Script*

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
</table>



<a name="loio021180336add475bbd712b0ce5d393c1__section_knq_5f3_vdb"/>

## Input

None.



<a name="loio021180336add475bbd712b0ce5d393c1__section_swc_cg3_vdb"/>

## Output

None.



<a name="loio021180336add475bbd712b0ce5d393c1__section_gd5_pd5_zdb"/>

## Basic Examples

> ### Example:  
> The following code snippet counts all incoming messages on the port named “input” and writes the count to the port named “output”:
> 
> ```
> counter = 0
> 
> def on_input(data):
>     global counter
>     counter += 1
>     api.send("output", counter)
> 
> api.set_port_callback("input", on_input)
> ```
> 
> The “output” port of an operator that contains this example code snippet is of type `int64` because the variable `counter` is of Python type `int`. For more information about how to choose your port types, see the section [Correspondence Between Modeler Types and Python Types](python3-operator-0211803.md#loio021180336add475bbd712b0ce5d393c1__section_flz_csp_ywb).

> ### Example:  
> Use `api.set_port_callback` to wait for two input ports to receive data before calling the handler.
> 
> ```
> def on_input(data1, data2):
>     api.send("output", data1 + data2)
> 
> api.set_port_callback(["input1", "input2"], on_input)
> ```





### api.send\(port, data\)

This API sends 'data' to an outport named 'port'.

**Arguments**


<table>
<tr>
<td valign="top">

`port (str)`

</td>
<td valign="top">

The name of the output port.

</td>
</tr>
<tr>
<td valign="top">

`data (...)`

</td>
<td valign="top">

The object to send.

</td>
</tr>
</table>



<a name="loio021180336add475bbd712b0ce5d393c1__section_crn_bdb_msb"/>

## Port Callbacks



### api.set\_port\_callback\(ports, callback\)

This API associates input \`ports\` to the \`callback\`. The API calls \`callback\` only when there are messages in all \`ports\`. If the operator calls `api.set_port_callback(ports, callback)` multiple times for the same port group, the operator replaces the old \`callback\` with a new \`callback\`.

**Limitations:**

-   You can't overlap different port groups.
-   You can't reuse the same callback function in different port groups.

**Arguments**


<table>
<tr>
<td valign="top">

`ports (str|list[str])`

</td>
<td valign="top">

The input ports to associate with the callback. Enter ports in one of the following ways:

-   A string `(str)` to associate the callback to a single port.
-   A list of strings `(list[str])` with the name of each port to associate.



</td>
</tr>
<tr>
<td valign="top">

`callback (func[…])`

</td>
<td valign="top">

A callback function with the same number of arguments as elements in 'ports', or a variable length argument. The API passes arguments to the 'callback' in the same order as the corresponding ports in the 'ports' list.

</td>
</tr>
</table>

To reuse the same callback function in multiple port groups, use a function that returns your function of interest.

> ### Example:  
> When you use a function that returns your function of interest, a new function is generated with a different ID each time, but the callback behavior remains the same.
> 
> ```
> def get_my_callback():
>   def my_callback(data):
>       # some code here
>   return my_callback
> 
> api.set_port_callback("inport1", get_my_callback())
> api.set_port_callback("inport2", get_my_callback())
> ```



### api.remove\_port\_callback\(callback\)

This API deregisters the 'callback' function. If the 'callback' function doesn't exist, the method exits quietly.

**Arguments**


<table>
<tr>
<td valign="top">

`callback`

</td>
<td valign="top">

The callback function to remove.

</td>
</tr>
</table>



<a name="loio021180336add475bbd712b0ce5d393c1__section_q4j_c2b_msb"/>

## Generators

Generators are functions that run before the start of the event processing loop. Generator functions run in the order in which you add them to the script.

> ### Example:  
> The following code snippet produces values 0,1,2,3,4,5 on the output port 'output'.
> 
> ```
> counter = 0
> 
> def gen():
>     global counter
>     for i in range(0, 3):
>         api.send("output", counter)
>         counter += 1
> 
> api.add_generator(gen)
> api.add_generator(gen)
> ```



<a name="loio021180336add475bbd712b0ce5d393c1__section_x5d_lfb_msb"/>

## Timers



### api.add\_timer\(period, callback\)

With this API, add multiple distinct periodic callbacks. If you add a callback that was already added, the function replaces the old 'period' with the new 'period' value.

Timer APIs aren't preemptive. Therefore, the given interval provides only the lower bound of the interval at which the Python3 operator calls the timer function. When you set the 'period' value to zero, the Python3 operator calls the callback as fast as possible.

To create two callbacks with identical behavior to run simultaneously, create one of the following objects:

-   Two functions with identical bodies.
-   A factory function that defines an inner function and returns it.

    Each time the operator calls the factory function, it returns a new function with a different ID, but with identical behavior.

    To view an example of a factory function, see the example in the [Port Callbacks](python3-operator-0211803.md#loio021180336add475bbd712b0ce5d393c1__section_crn_bdb_msb) section.


**Arguments**


<table>
<tr>
<td valign="top">

`callback (func)`

</td>
<td valign="top">

The callback function to call every \`milliseconds\`.

</td>
</tr>
<tr>
<td valign="top">

`period (str)`

</td>
<td valign="top">

The period between the calls of the \`callback\`. The API passes the period as a string.

> ### Example:  
> A period string of `-1.3h3m2us` means minus \(1.3 hours 3 minutes and 2 microseconds\), which the operator converts to -\(1.3\*3600 + 3\*60 + 2\*1e-6\) = -4860.000002 seconds.

Available suffixes are as follows:

-   h = hours
-   m = minutes
-   s = seconds
-   ms = milliseconds
-   us = microseconds
-   ns = nanoseconds

If you use multiple units in your input, ensure that you enter them in order from the largest unit \(h\) to the smallest unit \(ns\) as applicable.

> ### Example:  
> The value "2h3s" is allowed, but "3s2h" isn't allowed.

The string “0” doesn't require a unit of time suffix, and signs are optional. The function allows signs only in the beginning of the string. Enter the string “0” as one of the following examples:

-   `0`
-   `+0`
-   `-0`



</td>
</tr>
</table>

> ### Example:  
> The following code snippet produces a value 0,1,2... on port “output” until graph shutdown.
> 
> ```
> counter = 0
> 
> def t1():
>     global counter
>     api.send("output", counter)
>     counter += 1
> 
> api.add_timer("1s", t1)
> ```



### api.remove\_timer\(callback\)

This API deregisters the timer callback.

**Arguments**


<table>
<tr>
<td valign="top">

`callback (func)`

</td>
<td valign="top">

The callback function to remove.

</td>
</tr>
</table>



### api.update\_timer\(period, callback\)

This API updates the period of an existing callback. If the callback doesn't exist, the API doesn't issue an error.

**Arguments**


<table>
<tr>
<td valign="top">

`callback (func)`

</td>
<td valign="top">

The callback function for which the period is updated. If \`callback\` isn't registered, nothing changes.

</td>
</tr>
<tr>
<td valign="top">

`period (str)`

</td>
<td valign="top">

A number as a string that represents a new period to overwrite the old period value.

</td>
</tr>
</table>



<a name="loio021180336add475bbd712b0ce5d393c1__section_pkg_vwp_ywb"/>

## Shutdown Handlers

Shutdown handlers are functions that run after the operator stop event in the order in which you add them.

> ### Example:  
> If the script provides seven values to the “input” port, the following code snippet prints “shutdown1:7” and “shutdown2:7”:
> 
> ```
> counter = 0
> 
> def on_input(data):
>     global counter
>     counter += 1
> 
> api.set_port_callback("input", on_input)
> 
> def shutdown1():
>     print("shutdown1: %d" % counter)
> 
> def shutdown2():
>     print("shutdown2: %d" % counter)
> 
> api.add_shutdown_handler(shutdown1)
> api.add_shutdown_handler(shutdown2)
> ```



<a name="loio021180336add475bbd712b0ce5d393c1__section_tbs_dxp_ywb"/>

## Configuration API

The configuration API allows the operator to read configurations defined on the operator's editor view or added in the configuration pane in the graph editor.

> ### Example:  
> If you define a configuration named “foo”, access it by calling `api.config.foo`.

Configuration field names can't contain spaces. The “script” and “codelanguage” configuration fields don't appear in `api.config` because they are mandatory configuration parameters that that you shouldn't use. If you add a JSON object to a configuration field in the Modeler, it becomes a dictionary in Python.



<a name="loio021180336add475bbd712b0ce5d393c1__section_p2r_rxp_ywb"/>

## Logging

To log messages, use the following APIs based on the type of message:

-   <code>api.logger.info(“some text”)</code>
-   `api.logger.debug("some text")`
-   `api.logger.warn("some text")`
-   `api.logger.error("some text")`



<a name="loio021180336add475bbd712b0ce5d393c1__section_awh_vxp_ywb"/>

## Error Handling

The following table describes how to stop a graph and log an error properly when you use the Python3 operator.


<table>
<tr>
<th valign="top">

Solution

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Raise an exception.

</td>
<td valign="top">

Raise any exception inside a script so that the API logs the exception message and terminates the operator.

</td>
</tr>
<tr>
<td valign="top">

Call `api.propagate_exception(e)`.

</td>
<td valign="top">

Call `api.propagate_exception(e)` when the API issues the exception inside a thread that's different than the script's main thread. For `e`, enter the object that handles the exception correctly.

</td>
</tr>
</table>

> ### Note:  
> Don't write to `stderr`. Writing to `stderr` can have unintended consequences. Also, don't use `api.logger.fatal` or `api.logger.critical`, because they cause the graph to stop.



<a name="loio021180336add475bbd712b0ce5d393c1__section_hkf_myp_ywb"/>

## Halting Execution

Stop a running graph in one of the following ways:

-   Stop a running graph with an error: Follow the instructions in the [Error handling](python3-operator-0211803.md#loio021180336add475bbd712b0ce5d393c1__section_awh_vxp_ywb) section.
-   Stop a running graph without an error: Configure the Python3 operator to send a signal to a Graph Terminator operator.
-   Stop only the operator execution without stopping the whole graph: Deregister all of the operator callbacks.

    > ### Note:  
    > Stopping a single operator can stop the whole data flow in the graph.


When you halt a running graph, don't use the following Python commands:

-   `sys.exit(code)`: affects only the current Python thread.
-   `os._exit(code)`: causes the whole Python process to stop and the graph to stop with an error.

    > ### Note:  
    > To stop the whole graph with an error, follow the instructions in the [Error handling](python3-operator-0211803.md#loio021180336add475bbd712b0ce5d393c1__section_awh_vxp_ywb) section.




<a name="loio021180336add475bbd712b0ce5d393c1__section_kh2_s1q_ywb"/>

## repo\_root and subengine\_root

Use the following APIs to access the `repo_root` and `subengine_root` path respectively:

-   `api.repo_root`
-   `api.subengine_root`



<a name="loio021180336add475bbd712b0ce5d393c1__section_i4y_t1q_ywb"/>

## graph\_name, graph\_handle, and group\_id

Access the `graph_name`, `graph_handle`, and `group_id` values by using the following APIs respectively:

-   `api.graph_name`
-   `api.graph_handle`
-   `api.group_id`

The following table describes each value.


<table>
<tr>
<td valign="top">

`graph_name`

</td>
<td valign="top">

An identifier for a saved graph, such as `com.sap.dataGenerator`.

</td>
</tr>
<tr>
<td valign="top">

`graph_handle`

</td>
<td valign="top">

A unique identifier for the graph instance. The Modeler uses the term “Runtime Handle” instead of `graph_handle`.

</td>
</tr>
<tr>
<td valign="top">

`group_id`

</td>
<td valign="top">

A unique identifier for the group in which the operator is running.

</td>
</tr>
</table>



<a name="loio021180336add475bbd712b0ce5d393c1__section_n2h_v1q_ywb"/>

## multiplicity, multiplicity\_index

Use the following APIs to obtain `multiplicity` and `multiplicity_index` respectively:

-   `api.multiplicity`
-   `api.multiplicity_index`

The following table describes each value.


<table>
<tr>
<td valign="top">

`multiplicity`

</td>
<td valign="top">

The multiplicity of the operator group.

</td>
</tr>
<tr>
<td valign="top">

`multiplicity_index`

</td>
<td valign="top">

An integer in the range \[0, multiplicity\) that distinguishes the multiple instances of the operator.

</td>
</tr>
</table>



<a name="loio021180336add475bbd712b0ce5d393c1__inport_and_outport_section"/>

## Inports and Outports

To get the names of the input and output ports for the current operator instance, call the following APIs:

-   `api.get_inport_names()`
-   `api.get_outport_names()`

To check which inports or outports are connected, use the following APIs:

-   `api.is_inport_connected`
-   `api.is_outport_connected`

These APIs have the name of the port as key and a boolean indicating whether it's connected as the value.

> ### Example:  
> ```
> if api.is_outport_connected["outport1"]:
>     r = do_some_expensive_calculation()
>     api.send("outport1", r)
> ```



<a name="loio021180336add475bbd712b0ce5d393c1__section_vsh_dbq_ywb"/>

## Message Type

Access a message type in an API object as `api.Message`. Build the message type as `api.Message(body, attributes)`, where:

-   `body`: any object. This attribute is required.
-   `attributes`: dictionary of str to object, or None. The default value is None.

Access the `body` and `attributes` of a message object, `msg`, as `msg.body` and `msg.attributes` respectively.



<a name="loio021180336add475bbd712b0ce5d393c1__section_flz_csp_ywb"/>

## Correspondence Between Modeler and Python Types

Modeler types are allowed in the operator ports. For example, if you have an input port of type `blob`, then the Python object that you receive as argument to your port callback is of type `bytes`. If the output port of your operator has type `string`, send a Python object of type `str` in its output port.

The following table shows the Modeler types and the corresponding Python types.


<table>
<tr>
<th valign="top">

Modeler Type

</th>
<th valign="top">

Python Type

</th>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">

str

</td>
</tr>
<tr>
<td valign="top">

blob

</td>
<td valign="top">

bytes

</td>
</tr>
<tr>
<td valign="top">

int64

</td>
<td valign="top">

int

</td>
</tr>
<tr>
<td valign="top">

uint64

</td>
<td valign="top">

int

</td>
</tr>
<tr>
<td valign="top">

float64

</td>
<td valign="top">

float

</td>
</tr>
<tr>
<td valign="top">

byte

</td>
<td valign="top">

int

</td>
</tr>
<tr>
<td valign="top">

message

</td>
<td valign="top">

api.Message

</td>
</tr>
</table>

You can also set a Python operator port type to `python36`. However, with `python36`, you can connect this port only to other Python operators. `python36` can be useful to send Python-specific data types to other Python operators.

> ### Caution:  
> Connections between `python36` ports that cross group boundaries cause runtime errors and aren't allowed.



<a name="loio021180336add475bbd712b0ce5d393c1__section_zgs_rkb_msb"/>

## FAQ



### Where do I put initialization code for my operator?

If you use the run pattern in the following example, put the initialization code in the body of the script.

Execute the script once. Execute the callback function defined in the script multiple times, however, execute the commands from the script's outermost scope once:

> ### Example:  
> ```
> # Hypothetical script for Python3Operator
> 
> # In the operator's initialization, we might want to setup a connection
> # with a database, for example (`setup_connection` is an hypothetical function):
> db = setup_connection(api.config.host, api.config.port)
> 
> def my_callback_func(data):
>     global db
>     db.write(data)  # hypothetical call
> 
> api.set_port_callback("input", my_callback_func)
> ```

Alternatively, put the initialization code in a generator callback that is registered with `api.add_generator(func)`.

