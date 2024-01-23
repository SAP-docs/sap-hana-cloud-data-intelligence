<!-- loioad5efc3a42cd4795821f06ef01589eca -->

# JavaScript \(v2\)

The JavaScript \(v2\) operator allows you to execute JavaScript snippets within a graph.



It works similarly to the Javascript operator and supports the same API.

However, its execution differs from that of the Javascript operator when a blocking call to a Go function is performed \(for example, when sending data out from an output port\):

-   Javascript operator: blocks it until this blocking call returns. Until then, no part of the code can be executed

-   Javascript \(v2\) operator: allows another part of the code to be executed until the blocking call returns, when its allowInterrupt property is set to true. This behavior can be considered as a workaround for the missing asynchronous call method from the script code to a Go function in the Javascript operator API.




<a name="loioad5efc3a42cd4795821f06ef01589eca__section_c2h_lhd_xkb"/>

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

Code Language

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

Script

</td>
<td valign="top">

script

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The inline script to be executed. If the script starts with `file://` then the script file is executed.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Allow Interrupt

</td>
<td valign="top">

allowInterrupt

</td>
<td valign="top">

bool

</td>
<td valign="top">

Possibility to interrupt a blocking call to a Go function so that another part of the script code can be executed

Default: true

</td>
</tr>
</table>



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_b4x_f3d_xkb"/>

## Input

None



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_c5q_g3d_xkb"/>

## Output

None



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_onf_h3d_xkb"/>

## Creating a JavaScript Extension

To create an extension, follow the steps below:

1.  In the Modeler, go to the *Operators* tab and click the *\+* button to add a new operator extension.

2.  Select the base operator *Javascript Operator*, give it a name, and click *OK*.

3.  Navigate to your newly created extension and:

    1.  Add the desired input and output ports;

    2.  Add your JS script either as: a\) an inline script parameter in the extension configuration; b\) a separate file, using the the prefix `file://` to specify the file name in the script parameter.

    3.  Add your JavaScript snippet as an inline `script` parameter in the extension configuration or put the code into a separate file and use the prefix `file://` to specify the file name.


4.  Save your operator extension by clicking the disk icon.




<a name="loioad5efc3a42cd4795821f06ef01589eca__section_egd_5g3_xkb"/>

## Basic Example

The following example counts all incoming messages on the port `input` and writes the count to the port `output`.

```
var counter = 0

$.setPortCallback("input",onInput)

function onInput(ctx,s) {
    counter++
    $.output(counter)
}
```



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_ik3_f33_xkb"/>

## Generators

Generators are functions that are executed before the event processing loop starts

The example below produces values `0, 1, 2, 3, 4, 5` on the port output:

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



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_asq_v33_xkb"/>

## Timers

Timers are called at given intervals. Timers are not preemptive. Thus, the given interval provides only the lower bound of the interval at which the timer function is called. All timers are stopped prior to the execution of shutdown handlers.

This example produces the values `0, 1, 2...` on the port output until the graph is shut down.

```
var counter = 0

$.addTimer("1s",t1)

function t1(ctx) {
  $.output(counter)
  counter++
}
```

The function `addTimer()` returns a handler that can be used to disable the timer later through the function `removeTimer()`.

In this example, the function `t1()` is called three times. After that, the timer is removed and `t1()` is no longer called.

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



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_wfq_gj3_xkb"/>

## Handling messages

To modify a message, you should first make a copy of it. A helper function CopyMessage is provided for that sake. It only makes a shallow copy of the message and its attributes. Further changed values should be copied separately.

Assuming the operator has two input ports named in and in2 and an output port named out, both of type `message`:

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



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_cgc_zj3_xkb"/>

## String Coding API

String Coding API provides the possibility to convert a byte array encoded in UTF-8 into a string.

This example assumes that the input data is a message with its `body` being a byte array encoded in UTF-8 and converts this body into a string.

```
$.setPortCallback("input",onInput);
function onInput(ctx, s) {
    var bodystr = $.decodeString(s.Body);
    // do some processing on this bodystr string
    // ...
	$.output(bodystr);
}
```



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_dzg_ck3_xkb"/>

## Shutdown Handlers

Shutdown handlers are functions that are executed after event processing loop execution.

The example below outputs two values when the graph reaches its termination state. Each value represents the number of inputs received on the port input.

For example: if the operator receives 7 inputs, it outputs `7` and `7` when the graph is terminating:

```
cvar counter = 0

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



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_bxv_3k3_xkb"/>

## Configuration API

Configuration API provides the possibility to read the operator configuration values provided via graph description.

This example reads the operator configuration values myStr, myInt and myBool using a Generator function.

```
function gen(ctx) {
  $.str($.config.getString("myStr"))
  $.int($.config.getInt("myInt"))
  $.bool(""+$.config.getBool("myBool"))
}
$.addGenerator(gen)
```



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_obj_rk3_xkb"/>

## Graph Termination

The `done` function can be used to signal theoperator has finished its execution. This allows the graph to transition to completed if the other operators finished their execution successfully.

The fail function raises an error that sets the graph's status to *dead*.

The example below terminates the operator if the input value is even. It raises an error otherwise:

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



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_d3m_5k3_xkb"/>

## Handling Multiplicity

There are two functions that provide multiplicity-related information:

-   `$.getMultiplicity()`: returns the multiplicity of the operator's group.
-   `$.getMultiplicityIndex()`: returns an integer in the range `[0,$.getMultiplicity())` that can be used to distinguish the multiple instances of this operator.



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_izq_3l3_xkb"/>

## Send Message to Logging App

The log function enables users to send messages to the Data Intelligence Logging app. The parameters for this function are: `message`, `severity`, `messageCode`, and `details`. The `severity` parameter is optional and uses one of the following `enum` value:

-   logSeverity.ERROR

-   logSeverity.INFO

-   logSeverity.WARNING


The messageCode and details parameters are optional as well.

The function awaits the logging API call to finish. The client is set to a 10-second timeout for the client communication. If an error occurs or timeout is reached, the log message is logged in the tracer, with the same severity passed as parameter to the function.

The example below sends a message with `INFO` severity to the logging app, a value for the `messageCode` and details parameters.

```
$.log("message to log", $.logSeverity.INFO, "10003", "this is a detailed message to the log message");
```



<a name="loioad5efc3a42cd4795821f06ef01589eca__section_zwn_543_xkb"/>

## Subgraph \(Call a Graph From the JS Operator\)

The `instantiateGraph` function provides the possibility to call a graph from the JavaScript operator. You can provide parameters for the graph and handlers for output ports. `instantiateGraph` returns a graph object when graph is started or fail script execution.

The graph object has the following methods:

-   `wait`: block script execution until subgraph execution is finished. wait returns the graph status

-   `stop`: initiate subgraph termination. It returns without waiting for graph termination to be completed


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

