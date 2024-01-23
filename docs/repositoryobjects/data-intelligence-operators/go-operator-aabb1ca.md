<!-- loioaabb1ca8b30447f791ae255368dcdcbf -->

# Go Operator

The Go operator allows you to execute Go code within a graph.



It supports sending outputs from input handlers or functions that run periodically. Other functionality, such as logging, reading the operator configuration parameters, and sending responses to requests are supported and documented further below.



<a name="loioaabb1ca8b30447f791ae255368dcdcbf__section_sq1_nf3_vdb"/>

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

The programming language used in the code.

Default: "go"

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

Mandatory. The inline script to be executed. If the script starts with "file://", then the script file is executed.

Script File:

To reference a script file, the `script` configuration must start with the prefix `file://` followed by the file path.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Maximum Concurrency

</td>
<td valign="top">

maxConcurrency

</td>
<td valign="top">

int

</td>
<td valign="top">

The maximum number of concurrent requests that are handled per operator instance. The message order is preserved only when value is `1`.

Default: 1

</td>
</tr>
</table>



<a name="loioaabb1ca8b30447f791ae255368dcdcbf__section_knq_5f3_vdb"/>

## Input

None



<a name="loioaabb1ca8b30447f791ae255368dcdcbf__section_swc_cg3_vdb"/>

## Output

None



<a name="loioaabb1ca8b30447f791ae255368dcdcbf__section_wbv_gj4_zdb"/>

## Creating a Go Operator Extension

To create an extension, follow these steps:

1.  In the Modeler UI, go to the *Operators* tab and click the *\+* button to add a new operator extension.
2.  Select the base operator *Go Operator*, give it a name, and click *OK*.
3.  Add the desired input and output ports.
4.  Add your Go script either as:
    -   An inline `script` parameter in the extension configuration.
    -   As a separate file, using the prefix `file://` to specify the file name in the script parameter.

5.  Make sure your script belongs to `package main`.
6.  If you need something to run once on startup, define it inside `func Setup()`.
7.  To run a cleanup procedure once the graph shuts down, define the `func Cleanup()` with the required procedure.
8.  Define some function to deal with inputs \(documented below in the Input Handling Script section\) or to run periodically \(documented below in the Interval-Based function section\).
9.  Save your operator extension.



### Interval-Based Script

To build a basic interval-based script, you can follow this example:

```
package main

// here implement the function with the input port name, 
// so data coming from this input will call this function
func In(val interface{}){
	message := val.(map[string]interface{})
	body := message["Body"]
	attr := message["Attributes"].(map[string]interface{})
	encoding := message["Encoding"]

	// ...
}
```



### Input Handling Script

To build an input handling script, you can follow the example below.

When the operator has an input port named in and an output port named out, we may use the following script:

```
package main
var Out func(interface{})

// here implement the function with the input port name,
// so data coming from this input will call this function
func In(val interface{}){
    strValue := val.(string)
    strValue += "test"

    Out(strValue)
    // ...
}
```



<a name="loioaabb1ca8b30447f791ae255368dcdcbf__section_zq2_v1h_ghb"/>

## Script Details

The script must belong to the `package main`. It supports the following functionalities:



### Input Handling Script

To call a function based on an input incoming data, the function name should be the same as the port name, and data from that port will be sent through the function's parameter. The function must be exported \(for example, it begins with an upper case letter\).

All input received as parameters of the `interface{}` type, making necessary the usage of type assertion to manipulate it. To use message type, the value received through the input port should be converted to the type map\[string\]interface\{\}, then its members can be accessed with the keys `"Attributes"`, `"Encoding"` and `"Body"`, as in the following example.

Suppose the operator has an input port named in of `message` type::

```
package main

// here implement the function with the input port name,
// so data coming from this input will call this function
func In(val interface{}){
    message := val.(map[string]interface{})
    body := message["Body"]
    attr := message["Attributes"].(map[string]interface{})
    encoding := message["Encoding"]

    // ...
}
```



### Interval-Based Function

To create a function that runs periodically \(every X amount of milliseconds\), the global variable `Timer` must be set with the desired interval, and the function must be implemented as `func Tick()`.

The `Timer` value may be either an `int64` with the interval in milliseconds or a `time.Duration`.

Interval-based function example:

```
package main
var Timer int64 = 500

func Tick() {
	// function to be called every 500ms
	// changes here
}
```





### Sending Outputs

To send an output via an output port, a global exported variable must be declared, matching the desired output port's name. Its type must be `func(interface{})`.

Output functions example:

Suppose the operator has an input port named in:

```
package main

// sends a value to port "out1" when called
var Out1 func(interface{})
// sends a value to port "out2" when called
var Out2 func(interface{})
```



### Setup and Cleanup

To run a procedure before any other function from the script is called, the Setup function may be set. That function is **not** able to send outputs.

If some cleanup is needed when the graph is shutdown, the `Cleanup` function may be set. That function is **not** able to send outputs.

In the example below, the operator has an output port named `out`:

```
package main

var Log func(string)

func Setup() {
    Log("graph started")
}

func Cleanup() {
    Log("graph finished")
}
```



### Handling Messages

To modify a message, a copy of it should be done first. A helper function `CopyMessage` is provided for that sake. It only does shallow copy of the message and its attributes. Further changed values should be copied separately.

Suppose the operator has two input ports named in and in2 and an output port named out, both of type `message`:

```
package main

var CopyMessage func(map[string]interface{}) (map[string]interface{}, error)
var Out func(interface{}) 

func In(val interface{}){
    // the message must be copied before modifying it
    m, err := CopyMessage(val.(map[string]interface{}))
    if err != nil {
        panic(err)
    }

    // modifying an attribute reference
    // no further copy needed
    m["Attributes"].(map[string]interface{})["foo"] = "bar"

    // modifying the body's reference
    // no further copy needed
    m["Body"] = []byte("my-new-body")

    Out(m)
}

func In2(val interface{}){
    // the message must be copied before modifying it
    m, err := CopyMessage(val.(map[string]interface{}))
    if err != nil {
        panic(err)
    }

    attrs :=  m["Attributes"].(map[string]interface{})
    // modifying an attribute value
    // a copy is needed
    oldFoo := attrs["foo"].([]string)
    newFoo := make([]string, len(oldFoo)+1)
    // append "foo" to the slice
    copy(newFoo, oldFoo)
    newFoo[len(newFoo)-1] = "foo"
    

    // modifying the body's contents
    // a copy is needed
    oldBody := m["Body"].([]byte)
    newBody := make([]byte, len(oldBody))
    // set the first byte to 1
    copy(newBody, oldBody)
    newBody[0] = 0x01
    
    attrs["foo"] = newFoo
    m["Body"] = newBody

    Out(m)
}
```



### Handling Multiplicity

Two variables can be declared to obtain multiplicity-related information:

-   `Multiplicity`: the multiplicity of the operator's group.

-   `MultiplicityIndex`: an integer in the range \[0,Multiplicity\] that can be used to distinguish the multiple instances of this operator.


Both variables must be of type `int`.

Variable declaration:

```
var Multiplicity int
var MultiplicityIndex int
```



### Logging



To log messages during the Go operator execution, a function called `Log` must be defined and its parameter is string type. The formatted version `Logf` is also available with two parameters: `string, ...interface{}`. All logs will be added as Debug logs on the Modeler's tracer.

Logging example:

```
package main
var Log func(string)
var Logf func(string, ...interface{})

func Setup() {
	Log("starting go operator")
}

func In(val interface{}){
	strValue := val.(string)
	strValue += "test"
	Logf("input:%s", strValue)
	// ...
}
```

Error logging is also supported, following the same Log signature formats, with the following function names: `Error` or `Errorf`. Note that the error does not stop the graph, only writing the error to the tracer.



### Configuration

Configuration calls provide the ability to read the configuration parameters provided in the operator. The function parameter should be the property title.

The function \``AsObject`\` is also supported, and retrieves the whole operator configuration as a map, where each member points to a parameter with the configuration name as its key.

Configuration retrieval example:

Suppose we have configuration parameters with the following keys: `myStr`, `myInt`, `myBool`, `myObj`:

```
package main

var GetString func(string) string
var GetInt func(string) int
var GetBool func(string) bool
var GetObject func(string) map[string]interface{}
var AsObject func() map[string]interface{}

func In(val interface{}){
	strValue := GetString("myStr")
	intValue := GetInt("myInt")
 	boolValue := GetBool("myBool")
	objValue := GetObject("myObj")
	entireConfig := AsObject()

	if entireConfig["myStr"].(string) == strValue {
		// this is true as these are equivalent
	}
	// ...
}
```



### Operator Directory

To access the operator directory, a configuration value is available: workingDirectory. It can be accessed through the `GetString` function. Supposing the operator ID is `com.sap.system.myGoOp`, the following Go code would retrieve the operator path `files/vflow/operators/com/sap/system/myGoOp/`:

```
package main

var GetString func(string) string
func getDir() {
    workingDir := GetString("workingDirectory")
}
```



### Message Response

> ### Note:  
> This function is deprecated and it will be removed in next versions.

`SendResponse` sends either a message response or error as the response to a message request, and may be called from the Go script.

Message response example:

```
package main

var SendResponse func(map[string]interface{}, map[string]interface{}, error)

func Input(val interface{}){
	message := val.(map[string]interface{})
	body := message["Body"]
	attr := message["Attributes"].(map[string]interface{})
	encoding := message["Encoding"]

	SendResponse(message, message, nil)
	// ...
}
```



### Graph Handle

The `GetGraphHandle` function provides the current running graph handle as a string.

Graph handle example:

```
package main

var GetGraphHandle func() string

func Input(val interface{}){
	handle := GetGraphHandle()
	// ...
}
```



### Using External Libraries

The Golang plugin has a limitation that does not support loading external libraries as they were not built with the same Go version. To use external libraries, it is possible to add these libraries to the script and then search for the *Go Plugin Generator* graph. This graph takes those libraries and builds the plugin for your target graph, then, your target graph is able to run.

