<!-- loio0d9f2756389b46348b590dba254f5fa5 -->

# R Client

The R Client operator runs R code that you defined in the Rserve.



You can specify the code you want to run by writing an R script and adding callbacks by using the predefined `api` object.

For example, you can set a callback function `myFunc` that is called when you receive new data in the port `input1`, and then send data on port `output2` by writing `api$setPortCallback(c("input1"), c("output2"), "myFunc")`.

The functionalities offered by the `api` object are the following:

-   `api$setPortCallback(inports, outports, functionName)`

-   `api$addTimer(period, outports, functionName)`
-   `api$setSwitchCallback(inports, outports, functionName)`
-   `api$addShutdownHandler(functionName)`

Each of those functionalities will be discussed in later sections.

Your script will run during the initialization of the R Client operator.

For code that should run after the initialization, you can add and define callbacks in the script, by using methods from the `api` object such as: setPortCallback, addTimer, setSwitchCallback, and addShutdownHandler.

> ### Note:  
> This operator is built with R 4.1.0.



<a name="loio0d9f2756389b46348b590dba254f5fa5__section_att_jyx_kwb"/>

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

Script

</td>
<td valign="top">

scrip

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Inline script to be executed, or if the entered text starts with \\"file://\\", then it will be interpreted as the name of the script file to be executed.

Default: file://script.R

</td>
</tr>
<tr>
<td valign="top">

Switch Start Off

</td>
<td valign="top">

switchStartOff

</td>
<td valign="top">

boolean

</td>
<td valign="top">

In case a switch callback exists, then the other callbacks will be disabled from the graph's start if this field is true.

Default: true

</td>
</tr>
<tr>
<td valign="top">

Switch Affects Timer Callbacks

</td>
<td valign="top">

switchAffectsTimerCallbacks

</td>
<td valign="top">

boolean

</td>
<td valign="top">

In case a switch callback exists, then the timer callback will be affected by the state of the switch if this field is true \(the port callbacks are always affected\).

Default: true

</td>
</tr>
<tr>
<td valign="top">

Debug Mode

</td>
<td valign="top">

debugMode

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Set to true to get better error messages when connecting to an existing external Rserve. Performance may be affected when enabled.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Table Name by Outport

</td>
<td valign="top">

tableNameByOutport

</td>
<td valign="top">

array

</td>
<td valign="top">

A map from the outport name to the table name, which will be used when a data frame is sent to the given outport. If a data frame is sent on an outport that is not defined in this configuration, then the resulting `message.table` will have the table name filled as `'rclient' + <outportName>`.

Default: \[\]

</td>
</tr>
</table>



### Connection Parameters


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

Holds information about the services connections. Use connection type "Manual" only when using a Connection ID is not possible.

</td>
</tr>
<tr>
<td valign="top">

Configuration Type

</td>
<td valign="top">

configurationType

</td>
<td valign="top">

string

</td>
<td valign="top">

The type of connection information that will be used. `Manual` \(user input\) or `Configuration Manager` \(retrieved by the Connection Management service\).

Default: Manual

</td>
</tr>
<tr>
<td valign="top">

Connection ID

</td>
<td valign="top">

connectionID

</td>
<td valign="top">

string

</td>
<td valign="top">

The ID of the connection information to retrieve from the `Connection Management` service. The connection information needs to be of type RSERVE. If the Host field in your connection information is left empty, then a new Rserve will be launched automatically, and the rest of the credentials will be ignored. This field is only visible when `Configuration Type` is set to `Configuration Manager`.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Connection Properties

</td>
<td valign="top">

connectionProperties

</td>
<td valign="top">

object

</td>
<td valign="top">

This field is only visible when `Configuration Type` is set to `Manual`.

</td>
</tr>
<tr>
<td valign="top">

Host

</td>
<td valign="top">

host

</td>
<td valign="top">

string

</td>
<td valign="top">

Address of a running Rserve. If left empty, then an Rserve will be launched automatically, and a port will be found automatically.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Port

</td>
<td valign="top">

port

</td>
<td valign="top">

int

</td>
<td valign="top">

Port of the Rserve. If `Host` was left empty, then this field will be ignored.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Use TLS

</td>
<td valign="top">

useTLS

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Flags whether the connection should use TLS or not.

> ### Note:  
> If set to true, to be able to authenticate the external Rserve, you must upload the root certificate to the certificates folder at the *Certificates* tab in the *Connection Management* application.

Default: false

</td>
</tr>
<tr>
<td valign="top">

User

</td>
<td valign="top">

user

</td>
<td valign="top">

string

</td>
<td valign="top">

Username for authenticating in Rserve if required. If `Host` field is empty, then the supplied username will be ignored.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Password

</td>
<td valign="top">

password

</td>
<td valign="top">

string

</td>
<td valign="top">

Password for authenticating in Rserve if required. If `Host` field is empty, then the supplied password will be ignored.

Default: ""

</td>
</tr>
</table>



<a name="loio0d9f2756389b46348b590dba254f5fa5__section_phf_bby_kwb"/>

## Input

None.



<a name="loio0d9f2756389b46348b590dba254f5fa5__section_vpq_bby_kwb"/>

## Output

None.



<a name="loio0d9f2756389b46348b590dba254f5fa5__section_arn_hby_kwb"/>

## Allowed Types and \(Data Pipeline\)/R Type Equivalences



### Allowed Types in In/Out Ports

-   string
-   blob \(\[\]byte\)
-   float64
-   int64
-   uint64
-   arrays of the types above \(for example: \[\]string, \[\]\[\]float64, etc\)
-   byte
-   message
-   any



### \(Data Hub Modeler\)/R Type Equivalences


<table>
<tr>
<th valign="top">

Data Hub Modeler

</th>
<th valign="top">

R

</th>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">

character

</td>
</tr>
<tr>
<td valign="top">

blob

</td>
<td valign="top">

raw

</td>
</tr>
<tr>
<td valign="top">

float64

</td>
<td valign="top">

double/numeric \(64 bits\)

</td>
</tr>
<tr>
<td valign="top">

int64

</td>
<td valign="top">

integer \(signed 32 bits\)

</td>
</tr>
<tr>
<td valign="top">

uint64

</td>
<td valign="top">

integer \(signed 32 bits\)

</td>
</tr>
<tr>
<td valign="top">

slice or array

</td>
<td valign="top">

vector

</td>
</tr>
<tr>
<td valign="top">

byte

</td>
<td valign="top">

integer \(signed 32 bits\)

</td>
</tr>
<tr>
<td valign="top">

message\*

</td>
<td valign="top">

list\(Body,Attributes,Encoding\)

</td>
</tr>
<tr>
<td valign="top">

message.table\*\*

</td>
<td valign="top">

data frame

</td>
</tr>
</table>

\* message with field Encoding different than 'table'. Example of message creation in R: `m <- list(Body=11, Attributes=list(field1="foo"), Encoding="bar")`.

\*\* message with field Encoding equal to 'table'. In R, it is represented as a data frame.

> ### Note:  
> R Client operator will not warn or error if a data loss happens during numeric conversions between Go and R. For example, some uint64 values cannot be represented as a double nor as an integer in R. R Client does not specify what the result will be in those cases.

> ### Note:  
> Some R types are not supported during Modeler and R conversions, such as complex numbers, matrices, and factors. Sending them on the R Client output port may, at times, not cause an error, but the result is not defined.

The table shown in this section only covers types that can be used directly in the operator's ports. More information related to types that can be used in the inner fields of the `message` data type can be seen in the Go/R Type Equivalences and Conversions section.



<a name="loio0d9f2756389b46348b590dba254f5fa5__section_wj2_jcy_kwb"/>

## API Object Methods

> ### Note:  
> Adding new callbacks during other callback executions will have no effect. That is, it is not possible to add new callbacks after the operator's initialization.



### **api$setPortCallback\(inports, outports, functionName\)**

This method registers a callback named `functionName` that will be called when all ports in `inports` have data waiting to be read. The `outports` argument specifies the name of zero or more outports to which the returned values from `functionName` should be sent. The values returned by the function are expected to be returned with the list data type in R. So the last line of the function should contain something like: `list(output1=value1, output2=value2)`, where `output1` and `output2` are the outport names that were also specified in the `outports` argument of the method `api$setPortCallback`. If no outport was specified in `api$setPortCallback`, then the last line of the callback function can be anything because its return value will be ignored anyway.

If you specify outports for the callback, but in some calls you want to skip sending to the outport, then you can return NULL as the function return. For example, this is useful when you accumulate some data in a global variable for some calls, and then, in a later callback, you want to send the accumulated information. So in the first call you return NULL, and in the last call, you return `list(output=accumulated)`. In this manner, nothing is sent to the outport in the first call, only in the last one.

> ### Example:  
> ```
> acc = 0
> 
> on_input12add <- function(data1, data2) {
>     acc <<- acc + data1 + data2
> }
> 
> on_input12mult <- function(data1, data2) {
>     acc <<- acc * data1 * data2
>     list(output1=acc)
> }
> 
> on_input3pow <- function(data3) {
>     list(output1=acc^data3, output2=data3^data3)
> }
> 
> api$setPortCallback(c("input1", "input2"), c(), "on_input12add")
> 
> api$setPortCallback(c("input1", "input2"), c("output1"), "on_input12mult")
> 
> api$setPortCallback(c("input3"), c("output1", "output2"), "on_input3pow")
> ```

The script above has three callbacks: `on_input12add`, `on_input12mult`, and `on_input3pow`. Both `on_input12add` and `on_input12mult` functions wait for data to be available in the port group \(`input1`, `input2`\). When the data becomes available, the data from `input1` is passed to the first argument of the callbacks, and the data from `input2` is passed to the second argument of the callback. When more than one callback is associated with a port group \(as in this case\), the callbacks are executed sequentially in the order that the callbacks were added in the script.

The callback `on_input3pow` is associated with a port group that is disjoint from the previous one. In this case, the port group consists of just one input port `input3`. Notice that the callback should be the name of a function variable that is in scope. Inport names should coincide with the name of an existing inport, and the number of ports in a port group needs to equal the number of arguments of the callback associated with this group. It is important to notice that all port groups cannot overlap. For example, you cannot add a callback associated with ports \(`in1`, `in2`\) and another associated with port \(`in1`\) or ports \(`in2`, `in3`\). However, it is allowed to add more than one callback to the same port group. The union of all port groups does not need to cover all existing input ports of the operator. That means that some input ports can be left unused.

The function `on_input12add` will add `acc` \(a global variable\) with `data1` and `data2`, and assign the result to `acc` again. Because the line `api$setPortCallback(c("input1", "input2"), c(), "on_input12add")` didn't specify output ports, the return value of `on_input12add` will be ignored. This callback's objective is just to update the `acc` global variable.

On the other hand, the returned value of `on_input12mult` is not ignored. Instead, the value on the returned list with key equal `output1` will be fed into the output port of the same name. This intent was signaled by specifying `"output1"` in the list of outports in the `setPortCallback` method. Notice that when we specify that, we always need to return an R list with a key for each output name in the last line of the callback.



### **api$addTimer\(period, outports, functionName\)**

This method registers a callback named `functionName`, which will be repeatedly called on every `period` unit of time. The `period` is passed as a string. For example, "1.3h3m2us" means \(1.3 hours, 3 minutes, and 2 microseconds\).

Available suffixes are: h, m, s, ms, us, ns. They represent hours, minutes, seconds, milliseconds, microseconds, and nanoseconds, respectively. Only the strings "0", "+0", "-0" are allowed to not have a unit of time suffix \(they are optional in these cases\). Signs are optional and are allowed just at the beginning of the string.

The `outports` argument specifies the name of zero or more outports to which the returned values from `functionName` should be sent. The values returned by the function are expected to be returned with the list data type in R. So the last line of the function should contain something like: `list(output1=value1, output2=value2)`, where `output1` and `output2` are the outport names that were also specified in the `outports` argument of the method `api$addTimer`. If no outport was specified in `api$addTimer`, then the last line of the callback function can be anything because its return value will be ignored.

If you specify outports for the callback, but in some calls you want to skip sending to the outport, then you can return NULL as the function return. For example, this is useful when you accumulate some data in a global variable for some calls, and then, in a later callback, you want to send the accumulated information. So in the first call, you return NULL and in the last call, you return `list(output=accumulated)`. In this manner, nothing is sent to the outport in the first call, only in the last one.

> ### Example:  
> ```
> counter <- 0
> 
> t1 <- function() {
>     counter <<- counter + 1
>     list(output=counter)
> }
> 
> api$addTimer("1s", c("output"), "t1")
> ```

The above example produces values 1,2,3... on every second on outport `output` until the graph shutdown.



### **api$setSwitchCallback\(inports, outports, functionName\)**

This method adds a callback that can control the switch variable. When the switch is 'on', all other callbacks become enabled. When the switch is 'off', all other callbacks become disabled, and no data will be consumed in their ports.

The callback `functionName` added with `setSwitchCallback` will always need to return a boolean indicating what value the switch should assume. For example, suppose that you added a switch callback as:

```
api$setSwitchCallback(inports=c("inputX", "inputY"), outports=c("outputA",
      "outputB"), "foo")
```

Then the function `foo` should look like this:

> ### Example:  
> ```
> foo <- function(dataX, dataY) {
>     out1 <- dataX + dataY
>     out2 <- dataX * dataY
>     if (dataX %% dataY == 0) {
>         position <- FALSE
>     } else {
>         position <- TRUE
>     }
>     list(switchPosition=position, outputA=out1, outputB=out2)
> }
> ```

So the last line of switch callback always needs to have the keyword `switchPosition` in the returned list. Notice that the boolean returned will not be sent in any outport unless you include a port called 'switchPosition' of type `byte` in the operator and also specify this port in the `outports` parameter of the `api$setSwitchCallback` method. In case you specify, then the boolean will be converted to a byte and sent in the 'switchPosition' port, in addition to being used internally to set the value of the switch.

There are two operator configuration parameters related to the switch callback: `switchStartOff` and `switchAffectTimerCallbacks`. If `switchStartOff` is set to true, then the switch will start in the off position when the graph is started. The `switchAffectTimerCallbacks` configuration indicates whether the switch should affect \(block or unblock\) the timer callbacks too. On the other hand, the port callbacks are always affected, and the shutdown and switch callbacks are never affected by the switch position. That is the shutdown and switch callbacks are always enabled \(unblocked\).

Differently than `api$setPortCallback`, `api$setTimer`, and `api.addShutdownHandler`, `api$setSwitchCallback` can set only one callback. If you use the method more than once, the first callback will be replaced by the new one.



### **api$addShutdownHandler\(functionName\)**

This method will register the callback `functionName` to be called upon the graph's shutdown. If more than one callback is added they will be called sequentially in the order that they were added in the script.

R Client will try to execute all shutdown callbacks even when the operator is being stopped due to an error. Also, if one shutdown callback fails, the next ones will still run. R Client will only not try to run the shutdown callbacks when Rserve fails or if an error happens before the shutdown callbacks registration is completed.

> ### Example:  
> ```
> counter <- 0
> 
> on_input <- function(data) {
>     counter <<- counter + 1
> }
> 
> api$setPortCallback(c("input"), c(), "on_input")
> 
> shutdown1 <- function() {
>     cat("shutdown1: ", counter)
> }
> 
> shutdown2 <- function() {
>     cat("shutdown2: ", counter)
> }
> 
> api$addShutdownHandler("shutdown1")
> api$addShutdownHandler("shutdown2")
> ```

The above example prints "shutdown1: 7" and "shutdown2: 7" if 7 values have been provided on `input` port before the graph stops.



<a name="loio0d9f2756389b46348b590dba254f5fa5__section_ytk_sdy_kwb"/>

## Log Messages

If the **Host** configuration is left empty, then Rserve will be launched inside the graph's container, and R Client will be able to log with `DEBUG` level any message sent to Rserve´s STDOUT. R´s `print` function can be used to send messages to Rserve´s STDOUT.



<a name="loio0d9f2756389b46348b590dba254f5fa5__section_uth_5dy_kwb"/>

## Error Messages

If you leave the **Host** configuration empty, then Rserve will be launched inside the graph's container, and R Client will be able to save the STDERR stream of the Rserve process. In this case, if a failure happens, the accumulated STDERR stream will be concatenated to the error message shown in the UI. Notice that having **Debug Mode** equal to true may change what Rserve prints in STDERR. Sometimes it may be useful to set **Debug Mode** to false because it may cause STDERR to show new information.

When using an external Rserve by filling the **Host** configuration, the R Client will not be able to save Rserve's STDERR. In this case, the user can only resort to enabling **Debug Mode** for improving the error messages.



<a name="loio0d9f2756389b46348b590dba254f5fa5__section_pqq_wdy_kwb"/>

## Go/R Type Equivalences and Conversions

This section is useful if you are connecting R Client with a script Go operator.



### **Message Type**

The Go message type can be represented in R either as a generic `list` object or as a `data.frame`.

A non-`message.table` in Go will be represented as a `list` in R with the following fields: Body, Attributes, Encoding. The `Body` field can hold any R object that can be serialized to Go \(see `(Data Hub Modeler)/R Type Equivalences` section\). The `Attributes` should be an R `list` mapping field names to R objects. The `Encoding` should be a `character` vector.

> ### Note:  
> Although `bool` is not allowed as a port type, data of this type can be placed inside a message, and its equivalent R type is `logical`.



### **Message Table**

A `message.table` in Go has to follow a certain [format](https://github.wdf.sap.corp/velocity/vflow/blob/60f221d56d7be6bcdb0d13aa9754326014f56c17/src/stdlib/operators/com/sap/system/rClient4/service/v1/parse/readme/general/docu/table/README.md), and it is automatically converted to a `data.frame` when sent to R Client. A `data.frame` is also converted to a message.table when received from R Client. If the encoding field of the message is different than "table", then the equivalent type in R will be a `list` with the fields Body, Attributes, and Encoding.

In a `message.table`, we assume the type of each column is constant. In the next two subsections, we show how the data in the columns of a `message.table` are converted to their R equivalent and how the data in the columns of an R `data.frame` are converted to their Go equivalent. Currently, only the following R types for `data.frames` columns are supported when it is sent to the R Client outport: `logical`, `character`, `integer`, and `double`.

**Go `message.table` to R `data.frame`**

When a `message.table` is sent to R, the `class` field, on the column metadata of the message header, is ignored. The conversion is solely based on the Go type of the data on the table cells. The table below shows the mapping of the type of the columns of a `message.table` to the ones of an R `data.frame`.


<table>
<tr>
<th valign="top">

Go

</th>
<th valign="top">

R

</th>
</tr>
<tr>
<td valign="top">

bool

</td>
<td valign="top">

logical

</td>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">

character

</td>
</tr>
<tr>
<td valign="top">

float32 or float64

</td>
<td valign="top">

double \(64 bits\)

</td>
</tr>
<tr>
<td valign="top">

int\*

</td>
<td valign="top">

integer \(signed 32 bits\)

</td>
</tr>
</table>

\* `int` refers to the following Go types: `int8`, `uint8`, `int16`, `uint16`, `int32`, `uint32`, `int64`, `uint64`, `int`, and `uint`.

> ### Example:  
> ```
> map[string]interface{}{
>     "Body": []interface{}{
>         []interface{}{"alk", uint64(3), true, 1.3},
>         []interface{}{"", int8(-2), false, math.Inf(-1)},
>     },
>     "Attributes": map[string]interface{}{
>         "table": map[string]interface{}{
>             "version": int16(1),
>             "columns": []interface{}{
>                 map[string]interface{}{"name": "stringCol"},
>                 map[string]interface{}{"name": "intCol"},
>                 map[string]interface{}{"name": "boolCol"},
>                 map[string]interface{}{"name": "doubleCol"},
>             },
>         },
>     },
>     "Encoding": "table",
> }
> ```

is converted to

```
data.frame(stringCol=c("alk", ""), intCol=c(3L, -2L), boolCol=c(TRUE, FALSE),
      doubleCol=c(1.3, -Inf), stringsAsFactors=FALSE)
```

**R `data.frame` to Go `message.table`**

When an R `data.frame` is sent to Go, it will be converted to a `message.table` with the `class` field automatically filled for each column metadata, and the data on its body will be converted according to the mapping below:


<table>
<tr>
<th valign="top">

R

</th>
<th valign="top">

Go

</th>
<th valign="top">

Class

</th>
</tr>
<tr>
<td valign="top">

logical

</td>
<td valign="top">

bool

</td>
<td valign="top">

bool

</td>
</tr>
<tr>
<td valign="top">

character

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
</tr>
<tr>
<td valign="top">

double \(64 bits\)

</td>
<td valign="top">

float64

</td>
<td valign="top">

float

</td>
</tr>
<tr>
<td valign="top">

integer \(signed 32 bits\)

</td>
<td valign="top">

int32

</td>
<td valign="top">

integer

</td>
</tr>
</table>

The table name field of the resulting `message.table` will be either `'rclient' + <outportName>` or the name specified in the configuration field `Table Name By Outport`. We also set all columns as `nullable`.

> ### Example:  
> ```
> data.frame(stringCol=c("alk", ""), intCol=c(3L, -2L), boolCol=c(TRUE, FALSE),
>       doubleCol=c(1.3, -Inf), stringsAsFactors=FALSE)
> ```
> 
> is converted to
> 
> ```
> map[string]interface{}{
>     "Body": []interface{}{
>         []interface{}{"alk", int32(3), true, 1.3}, []interface{}{"", int32(-2), false, math.Inf(-1)},
>     },
>     "Attributes": map[string]interface{}{
>         "name": "rclientoutput"
>         "table": map[string]interface{}{
>             "version": int64(1),
>             "columns": []interface{}{
>                 map[string]interface{}{"name": "stringCol", "class": "string", "nullable": true},
>                 map[string]interface{}{"name": "intCol", "class": "integer", "nullable": true},
>                 map[string]interface{}{"name": "boolCol", "class": "bool", "nullable": true},
>                 map[string]interface{}{"name": "doubleCol", "class": "float", "nullable": true},
>             },
>         },
>     },
>     "Encoding": "table",
> }
> ```

The above example assumes the `Table Name By Outport` field was not specified for the used outport and that the used outport was named `output`. Observe that in the `data.frame` creation in R we specified `stringsAsFactors=FALSE`. This is necessary since, by default, data frame creation in R converts strings to factors, and we currently do not support factors in conversions to `message.table`.

**Non-Table-Message Go to R Conversions Examples**


<table>
<tr>
<th valign="top">

Go

</th>
<th valign="top">

R

</th>
</tr>
<tr>
<td valign="top">

"abcd"

</td>
<td valign="top">

"abcd"

</td>
</tr>
<tr>
<td valign="top">

\[\]string\{"al", "alkj"\}

</td>
<td valign="top">

c\("al", "alkj"\)

</td>
</tr>
<tr>
<td valign="top">

\[\]\[\]string\{\{"al", "alkj"\}, \{"al2", "alkj2"\}\}

</td>
<td valign="top">

list\(c\("al", "alkj"\), c\("al2", "alkj2"\)\)

</td>
</tr>
<tr>
<td valign="top">

int64\(1\)

</td>
<td valign="top">

1L

</td>
</tr>
<tr>
<td valign="top">

1.0

</td>
<td valign="top">

1.0

</td>
</tr>
<tr>
<td valign="top">

\[\]\[\]float64\{\{1, 2\}, \{3,4\}\}

</td>
<td valign="top">

list\(c\(1, 2\), c\(3, 4\)\)

</td>
</tr>
<tr>
<td valign="top">

\[\]byte\{1, 2, 3\}

</td>
<td valign="top">

as.raw\(c\(1,2,3\)\)

</td>
</tr>
<tr>
<td valign="top">

map\[string\]interface\{\}\{"Body": 3, "Attributes": nil, "Encoding": "foo"\}

</td>
<td valign="top">

list\(Body=3, Attributes=list\(\), Encoding="foo"\)

</td>
</tr>
<tr>
<td valign="top">

nil

</td>
<td valign="top">

NA

</td>
</tr>
</table>



### **Non-Data-Frame R to Go Conversions**

This section is divided into two subsections. The first shows how conversions are done when the target Go type is known. The second covers the case when the target Go type is not known \(when the output port is of type `any` or when data is inside the body of a `message`\).

**Target Go Type Is Known**

In this context, the output port of the R Client indicates the target Go type for the R object to be converted to.

**Examples R to Go \(Known Target Type\):**

-   outport type `uint64`:


    <table>
    <tr>
    <th valign="top">

    R
    
    </th>
    <th valign="top">

    Go
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    1L
    
    </td>
    <td valign="top">
    
    uint64\(1\)
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    2.7
    
    </td>
    <td valign="top">
    
    uint64\(2\)
    
    </td>
    </tr>
    </table>
    
-   outport type `int64`:


    <table>
    <tr>
    <th valign="top">

    R
    
    </th>
    <th valign="top">

    Go
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    \-1L
    
    </td>
    <td valign="top">
    
    int64\(-1\)
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    \-2.7
    
    </td>
    <td valign="top">
    
    int64\(-2\)
    
    </td>
    </tr>
    </table>
    
-   outport type `float64`:


    <table>
    <tr>
    <th valign="top">

    R
    
    </th>
    <th valign="top">

    Go
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    1L
    
    </td>
    <td valign="top">
    
    float64\(1.0\)
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    2.7
    
    </td>
    <td valign="top">
    
    float64\(2.7\)
    
    </td>
    </tr>
    </table>
    
-   outport type `[]uint64`:


    <table>
    <tr>
    <th valign="top">

    R
    
    </th>
    <th valign="top">

    Go
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    1.3
    
    </td>
    <td valign="top">
    
    \[\]uint64\{1\}
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    c\(1.3\)
    
    </td>
    <td valign="top">
    
    \[\]uint64\{1\}
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    c\(1.3, 2.7\)
    
    </td>
    <td valign="top">
    
    \[\]uint64\{1, 2\}
    
    </td>
    </tr>
    </table>
    

**Target Go Type Is Unknown**

The target Go type might not be known when the port type remains `any` even after the port types are propagated or when the data is inside the body of a message. In those cases, all numeric and vector of numeric types in R will be converted to `float64` and slice of `float64` in Go, respectively \(except in `data.frame` to `message.table` conversions where `double` is converted to `float64`, but `integer` is converted to `int32`\). Singletons vectors in R \(`c(1)`\) will be converted to scalars in Go \(`1.0`\). On the other hand, singleton lists \(`list(1)`\) will be converted to a singleton slice in Go \(`[]float64{1.0}`\).

**Examples R to Go \(Unknown Target Type\):**


<table>
<tr>
<th valign="top">

R

</th>
<th valign="top">

Go

</th>
</tr>
<tr>
<td valign="top">

1L

</td>
<td valign="top">

float64\(1\)

</td>
</tr>
<tr>
<td valign="top">

2.7

</td>
<td valign="top">

float64\(2.7\)

</td>
</tr>
<tr>
<td valign="top">

c\(1.3\)

</td>
<td valign="top">

float64\(1.3\)

</td>
</tr>
<tr>
<td valign="top">

list\(1\)

</td>
<td valign="top">

\[\]float64\{1\}

</td>
</tr>
<tr>
<td valign="top">

c\(1.3, 2.7\)

</td>
<td valign="top">

\[\]float64\{1.3, 2.7\}

</td>
</tr>
<tr>
<td valign="top">

list\(1.3, 3L\)

</td>
<td valign="top">

\[\]float64\{1.3, 3.0\}

</td>
</tr>
<tr>
<td valign="top">

list\(Body=3, Attributes=list\(\)\)

</td>
<td valign="top">

map\\\[string\\\]interface\{\}\{"Body": 3.0, "Attributes": nil\}

</td>
</tr>
<tr>
<td valign="top">

list\(c\(1,2,3\), c\(4,5,6\)\)

</td>
<td valign="top">

\[\]\[\]float64\{\{1, 2, 3\}, \{4, 5, 6\}\}

</td>
</tr>
<tr>
<td valign="top">

list\(c\(1,2,3\), c\("alkj"\)\)

</td>
<td valign="top">

\[\]interface\{\}\{\[\]float64\{1, 2, 3\}, "alkj"\}

</td>
</tr>
<tr>
<td valign="top">

c\("one","two","three"\)

</td>
<td valign="top">

\[\]string\{"one", "two", "three"\}

</td>
</tr>
<tr>
<td valign="top">

list\("one","two","three"\)

</td>
<td valign="top">

\[\]string\{"one", "two", "three"\}

</td>
</tr>
<tr>
<td valign="top">

NULL

</td>
<td valign="top">

nil

</td>
</tr>
<tr>
<td valign="top">

NA

</td>
<td valign="top">

nil

</td>
</tr>
<tr>
<td valign="top">

list\(1, "lakj", c\(2, 3, 4\), c\("alkj", "qoiu"\)\)

</td>
<td valign="top">

\[\]interface\{\}\{1.0, "lakj", \[\]float64\{2, 3, 4\}, \[\]string\{"alkj", "qoiu"\}\}

</td>
</tr>
<tr>
<td valign="top">

list\(list\(1L, "abc", 2.0\), list\(\), list\("def", 3\)\)

</td>
<td valign="top">

\[\]\[\]interface\{\}\{\{1.0, "abc", 2.0\}, \{\}, \{"def", 3.0\}\}

</td>
</tr>
<tr>
<td valign="top">

list\(c\(1\), c\(1, 2\), c\(3, 4\)\)

</td>
<td valign="top">

\[\]interface\{\}\{1.0, \[\]float64\{1, 2\}, \[\]float64\{3, 4\}\}

</td>
</tr>
</table>

> ### Note:  
> In the last example above that `c(1)` is converted to `1.0` and not to `[]float64{1.0}`. This is because singleton vectors in R are converted to scalars in Go.



<a name="loio0d9f2756389b46348b590dba254f5fa5__section_vyj_t3y_kwb"/>

## Docker Tags

The default R Client operator already comes with three tags: "rserve", "rjsonlite", and "rmsgpack". Those are needed to select the right docker image for the container where the operator's group will run. Those tags are only relevant when the user leaves the **Host** configuration field empty and thus causing a new Rserve process to be launched inside the operator's group container. If you are going to connect to an already existing Rserve by specifying the **Host** configuration, then you don't need those tags. You can remove those tags by creating a new operator that extends the R Client operator. Removing the tags is not mandatory when connecting to an external Rserve, but it is recommended since it will lower the requirements for the docker image selected for the operator's group. If your external Rserve doesn't already have the `jsonlite` and `msgpack` packages installed, they will be installed the first time you run the R Client operator connected to that **Host**. The graph may take a while to start due to the installation time of those packages in your external Rserve.

