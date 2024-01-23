<!-- loioa59151380fdc461e97cdb66c7d360ff0 -->

# JavaScript Operator

The JavaScript operator allows for execution of JavaScript snippets within a graph.



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_sq1_nf3_vdb"/>

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

codelanguage

</td>
<td valign="top">

codelanguage

</td>
<td valign="top">

string

</td>
<td valign="top">

The programming language used in the snippet.

Default: "javascript"

</td>
</tr>
<tr>
<td valign="top">

script

</td>
<td valign="top">

script

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The inline script to be executed. If the script starts with `file://`, then the script file is executed.

Default: ""

</td>
</tr>
</table>



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_knq_5f3_vdb"/>

## Input

None



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_pnn_dd3_xgb"/>

## Output

None



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_llw_bg4_zdb"/>

## Creating a JavaScript Extension

1.  Create an extension of the JavaScript component and add the desired in and out ports.
2.  Add your JavaScript snippet as an inline "script" parameter in extension configuration or put the code into a separate file and specify the filename with the prefix "`file://`" to reference it.

To create an extension, follow these steps:

1.  In the Modeler UI, go to the *Operators* tab and click the *\+* to add a new operator extension.
2.  Select the base operator *Javascript Operator*, name it, and click *OK*.
3.  Add the desired input and output ports.
4.  Add your JavaScript as one of the following:
    -   an inline script parameter in the extension configuration;

    -   as a separate file, using the prefix `file://` to specify the file name in the script parameter;


5.  Save your operator extension.



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_ggr_2g4_zdb"/>

## Basic Example

The following examples count all incoming messages on the port `input` and writes the count to the port `output`.

```
var counter = 0

$.setPortCallback("input",onInput)

function onInput(ctx,s) {
    counter++
    $.output(counter)
}
```



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_ebz_gg4_zdb"/>

## Generators

Generators are functions that will be executed before the event processing loop starts.

```
var counter = 0

$.addGenerator(gen)
$.addGenerator(gen)

function gen(ctx) {
    for (var i = 0; i < 3; i++ ) {
      $.output(counter)
      counter++
    }
}
```

This example will produce values `0`, `1`, `2`, `3`, `4`, `5` on the output port `output`.



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_dh3_kg4_zdb"/>

## Timers

Timers will be called at given intervals. Timers are not preemptive. Thus, the given interval provides only the lower bound of the interval at which the timer function will be called. All timers will be stopped prior to the execution of `shutdown handlers`.



### Timer-based function example

The example below produces the values `0`, `1`, `2`, and so on on the port `output` until the graph is shut down.

```
var counter = 0

$.addTimer("1s",t1)

function t1(ctx) {
  $.output(counter)
  counter++
}
```

The function `addTimer()` returns a handler that can be used to disable later through the function `removeTimer()`.



### Disabling a Timer

In the following example, the function `t1()` will be called three times. After that, the timer will be removed and `t1()` will not be called anymore.

```
var counter = 0

var timerId = $.addTimer("100ms",t1)

function t1(ctx) {
    counter++
    console.log("in t1() counter == ", counter)
    $.output(counter)

        if (counter == 3)
        $.removeTimer(timerId)
}
```



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_njy_fch_ghb"/>

## Handling Messages

To modify a message, a copy of it should be done first. A helper function `CopyMessage` is provided for that purpose. It does only a shallow copy of the message and its attributes. Further changed values should be copied separately.

Suppose the operator has two input ports named `in` and `in2` and an output port named out, both of type `message`:

```
$.setPortCallback("in", onIn)
$.setPortCallback("in2", onIn2)

function onIn(ctx,s) {
    // the message must be copied before modifying it
    var m = $.copyMessage(s);

    // modifying an attribute reference
    // no further copy needed
    m.Attributes["foo"] = "bar";

    // modifying the body's reference
    // no further copy needed
    m.Body = "my-new-body"

    $.out(m)
}

function onIn2(ctx,s) {
    // the message must be copied before modifying it
    var m = $.copyMessage(s);

    // modifying an attribute value
    // a copy is needed
    var oldFoo = m.Attributes["foo"];
    if (Array.isArray(oldFoo)) {
        var newFoo = oldFoo.slice() + "foo";
        m.Attributes["foo"] = newFoo;
    }

    // modifying the body's contents
    // a copy is needed
    // set the first value to 1
    var oldBody = m.Body;
    if (Array.isArray(oldBody)) {
        var newBody = oldBody.slice();
        newBody[0] = 0x01;
        m.Body = newBody;
    }

    $.out(m)
}
```



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_yrx_mg4_zdb"/>

## Shutdown Handlers

Shutdown handlers are functions that will be executed after event processing loop execution.

This example outputs two values when the graph reaches its termination state. Each value represents the number of inputs received on the port `input`.

For example, if the operator received seven inputs, it will output `7` and `7` when the graph is terminating.

```
var counter = 0

$.setPortCallback("input",onInput)

function onInput(ctx,s) {
    counter++
}

function shutdown(ctx) {
    $.output(counter)
}

$.addShutdownHandler(shutdown)
$.addShutdownHandler(shutdown)
```

This example outputs two values when the graph reaches its termination state. Each value represents the number of inputs received on the port `input`.



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_a2b_qg4_zdb"/>

## Configuration API

Configuration API provides the possibility to read configurations provided via graph description.

```
function gen(ctx) {
  $.str($.config.getString("str"))
  $.int($.config.getInt("int"))
  $.bool(""+$.config.getBool("bool"))
}
$.addGenerator(gen)
```

The example above will read the operator's configurations and provide the given values on the output ports.



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_kzn_bfd_fhb"/>

## Graph Termination

The `done` function can be used to signal this operator has finished its execution. This will allow the graph to transition to `completed` if the other operators have finished their execution successfully.

The `fail` function raises an error that sets the graph's status to `dead`. The message provided to fail is truncated after 64k characters.

The example below terminates a graph, succeeding if the received value from the port `input` is even, or failing otherwise:

```
$.setPortCallback("input", onInput)

function onInput(ctx,s) {
    v = parseInt(s)
    if (v % 2 === 0) {
      $.done()
    } else {
      $.fail("unexpected value received")
    }
}
```



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_fzc_jwf_ghb"/>

## Handling Multiplicity

There are two functions that provide multiplicity-related information:

-   `$.getMultiplicity()`: returns the multiplicity of the operator's group.
-   `$.getMultiplicityIndex()`: returns an integer in the range <code>[0<code>$.getMultiplicity()</code>]</code> that can be used to distinguish the multiple instances of this operator.



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_ibx_hz2_fhb"/>

## Message Response Handling

The `sendResponse` function provides the ability to send either a response or error message to the request-response initiating operator. This function is only valid if the incoming data is of type message and it contains the response callback as part of a request-response message exchange.

The example below sends a response or error depending on the current counter value.

```
var counter = 0

function onInput(ctx,s) {
    counter++
    if (counter < 100) {
        var msg = {};
        msg.Body = "pong " + counter;
        $.sendResponse(s, msg, null);
    } else {
        $.sendResponse(s, null, Error("Usage limit reached " + counter));
    }
}
```



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_xc2_4z2_fhb"/>

## Send Message to Logging App

The log function enables users to send messages to the SAP Data Intelligence Logging app. The parameters for this function are: `message`, `severity`, `messageCode`, and `details`. The `severity` parameter is optional and uses one of the following enum values:

-   `logSeverity.ERROR`
-   `logSeverity.INFO`
-   `logSeverity.WARNING`

The `messageCode` and `details` parameters are optional as well.

The function awaits the logging API call to finish. The client is set to a 10-second timeout for the client communication. If an error occurs or timeout is reached, the log message will be logged in the tracer, with the same severity passed as parameter to the function. Other errors will kill the graph. The Log API should provide strong guarantees.

The following example sends a message with `INFO` severity to the logging app, a value for the `messageCode` and `details` parameters.

```
$.log("message to log", $.logSeverity.INFO, "10003", "this is a detailed message to the log message");
```



<a name="loioa59151380fdc461e97cdb66c7d360ff0__section_ibn_flr_1fb"/>

## Subgraph \(Call a Graph From a JavaScript Operator\)

The `instantiateGraph` function provides the possibility to call a graph from the JavaScript operator. You can provide parameters for the graph and handlers for output ports. `instantiateGraph` returns a graph object when graph is started or fail script execution. The graph object has the following methods:

-   `wait` blocks script execution until subgraph execution is finished; `wait` returns the graph status.
-   `stop` initiates subgraph termination. It returns without waiting for graph termination to be completed.

```
$.addGenerator(gen)

// This example shows basic usage of a subgraph
// It calls a graph with a parameter, provides input to a port,
// checks a port's output and stops the graph

var graphName = "com.sap.demo.subgraph.call-and-wait.sub"
var subgraphInput = "subgraph-input "
var paramValue = "value1"
function gen(ctx) {
  // start subgraph
  var g
  try {
    g = $.instantiateGraph(graphName,
      {"param1": paramValue},
      // handle subgraph output port with name 'output'
      {"output":function(ctx,s){
          // check subgraph output
          if (s != subgraphInput + paramValue) {
              $.fail("Unexpected subgraph output: " + s + " Expected: " + prefix+paramValue)
          }
          // stop subgraph
          g.stop()
      }}
    )
  } catch(e) {
    $.fail(e.message)
    return
  }
  // write string in subraph input port with name 'input'
  g.input(subgraphInput)
  // wait for graph execution is finished
  status = g.wait()
  // check graph status
  if (status != $.graphStatus.completed) {
    $.fail("Subgraph is failed")
  } else {
    $.done()
  }
}
```

