<!-- loio0b6100b9ce244d18ab709fe06227fe23 -->

# Streaming Analytics Projects

This operator represents a streaming analytics project. The operator is based on streaming lite, which is a compact version of SAP HANA streaming analytics. As such, each instance of the operator starts an instance of the streaming lite server.



This streaming lite instance does not depend on SAP HANA in any way. If you wish to read from or write data to an SAP HANA database, you can do so by adding the Database Input or Output adapter into your streaming analytics project.

Streaming analytics is ideally suited for situations where data arrives as events happen, and where there is value in collecting, understanding, and acting on this data right away. Some examples of data sources that produce streams of events in real time include:

-   Sensors

-   Smart devices

-   Web sites \(click streams\)

-   IT systems \(logs\)

-   Financial markets \(prices\)

-   Social media


Data flows into streaming projects from various sources, such as adapters or operator ports that connect the sources to the streaming lite server. The streaming projects contain business logic, which they apply to the incoming data, typically in the form of continuous queries and rules. These streaming projects are entirely event-driven, turning the raw input streams into one or more derived streams that can be captured in a database, sent as alerts, posted to downstream applications, or streamed to live dashboards.

At its most basic level, a project consists of streams, windows, and adapters.

-   Adapters connect a stream or window to a data source or destination.

-   A stream processes incoming events without retaining and storing data, and produces output events according to an applied continuous query.

-   A window receives data but can also retain and store data. Incoming events can add, update, or delete rows in the window's table.


You can also define one or more input and output operator ports in your project to receive and send data.



## Configuration Parameters


<table>
<tr>
<th valign="top">

Title

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

script

</td>
<td valign="top">

string

</td>
<td valign="top">

Contains Continuous Computation Language \(CCL\), which specifies the functionality of the project. CCL is the primary event processing language of streaming analytics and is based on Structured Query Language \(SQL\).

Default: "file://script.ccl"

</td>
</tr>
<tr>
<td valign="top">

CCX

</td>
<td valign="top">

ccx

</td>
<td valign="top">

string

</td>
<td valign="top">

Already compiled CCL \(CCX\) that is used to start the project.

-   If this value is empty, the script property must have a value specified as that is then compiled into CCX and used to start the project.

-   If a value is provided, the script property value is ignored and the compiled CCX is used to start the project.


Default: ""

</td>
</tr>
<tr>
<td valign="top">

CCR

</td>
<td valign="top">

ccr

</td>
<td valign="top">

string

</td>
<td valign="top">

Optional runtime project configuration \(CCR\) file that governs specific runtime properties of a project.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Command Port

</td>
<td valign="top">

command port

</td>
<td valign="top">

string

</td>
<td valign="top">

If specified, this port number is used by the project to listen for commands. If the value is 0 or left empty, a random free port number is used instead.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Input Format

</td>
<td valign="top">

input format

</td>
<td valign="top">

string

</td>
<td valign="top">

The format used to parse rows received on input ports.

-   CSV: Incoming records need to be in comma-separated values \(CSV\) format and follow the RFC4180 standard. Headers are not supported. Multiple records can be batched together.

-   JSON: Input can be only a JSON array. Each of its elements can be either:

    -   A JSON array representing a data row where its elements are in the same order as the schema of the target input stream or window in the project CCL. If the input has opcodes parameter is set to true, the first array element must contain an opcode character.

    -   A JSON object whose keys are the column names in the schema of the target input stream or window in the project CCL. Spare keys are ignored. If the input has opcodes parameter is set to true, the JSON object must contain an `__opcode` field with an opcode character value specified.


Default: "CSV"

</td>
</tr>
<tr>
<td valign="top">

Output Format

</td>
<td valign="top">

output format

</td>
<td valign="top">

string

</td>
<td valign="top">

The format used to build rows that are sent on output ports.

-   CSV: Outgoing records are in CSV format and follow the RFC4180 standard. Headers are not included and multiple records are batched together according to the values specified in the output batch size and output batch timeout parameters.

-   JSON: Output is a JSON array that forms a batch of records. The size is based on the values specified in the output batch size and output batch timeout parameters. Each array element is either a JSON object or an array depending on the value of the JSON record type parameter.


Default: "CSV"

</td>
</tr>
<tr>
<td valign="top">

JSON Record Type

</td>
<td valign="top">

json record type

</td>
<td valign="top">

string

</td>
<td valign="top">

The type of JSON record to ouput for each outgoing data row.

-   Object: Each outgoing record is a JSON object whose keys are the column names in the schema of the source output stream or window in the project CCL. If the *add opcodes to output* parameter is set to true, the JSON object will contain an *<\_\_opcode\>* field with an opcode character value specified.

-   Array: Each outgoing record is a JSON array representing a data row. Its elements are in the same order as the schema of the source output stream or window in the project CCL. If the *add opcodes to output* parameter is set to true, the first array element contains an opcode character.


Default: "Object"

</td>
</tr>
<tr>
<td valign="top">

Input Has Opcodes

</td>
<td valign="top">

input has upcodes

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Specifies whether incoming data rows contain an opcode character. If set to `false`, the insert opcode value is used. If set to `true`, each incoming data row will include one of the following opcodes:

-   `i` \(insert\): Insert the record. Throw an error if a record with the same key already exists.

-   `u` \(update\): Update an existing record. Throw an error if a record with the specified key does not exist.

-   `d` \(delete\): Delete a record. Throw an error if a record with the specified key does not exist.

-   `p` \(upsert\): Insert the record if the key does not exist, update the record otherwise.

-   `s` \(safedelete\): Delete the record if it exists, do nothing if it doesn't exist.


Default: "true"

</td>
</tr>
<tr>
<td valign="top">

Add Opcodes to Output

</td>
<td valign="top">

add opcodes to output

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Specifies whether the outgoing data rows contain an opcode character.

Default: "true"

</td>
</tr>
<tr>
<td valign="top">

Output Batch Size

</td>
<td valign="top">

output batch size

</td>
<td valign="top">

string

</td>
<td valign="top">

Specifies how many outgoing rows, per output port, should be included in a batch. If the value is empty or set to less than 2 rows, each outgoing row is sent individually.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Output Batch Timeout \(ms\)

</td>
<td valign="top">

output batch timeout

</td>
<td valign="top">

string

</td>
<td valign="top">

Specifies how many milliseconds to collect output rows for a batch before sending out the current batch and starting a new one. If the value is left empty or is less than 10 milliseconds, the default timeout of 10000 milliseconds \(10 seconds\) is used. That is, the shortest duration you can specify is 10 milliseconds.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Stats Frequency \(sec\)

</td>
<td valign="top">

stats frequency

</td>
<td valign="top">

string

</td>
<td valign="top">

Specifies how often, in seconds, to print out an INFO level message with message flow statistics. For example, if set to 10 seconds, an INFO level message will print out every 10 seconds.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Hana Services

</td>
<td valign="top">

hana services

</td>
<td valign="top">

array

</td>
<td valign="top">

An array of objects containing connection parameters for SAP HANA databases that can be used as data services. To be able to access the data services from the project CCL, the name of each object needs to match the corresponding service property in the project CCL. All array elements can be either:

-   Manual: All required SAP HANA connection properties need to be specified in the properties editor.

-   Configuration Manager: Existing connections that are type `HANA_DB` and defined in Connection Management can be selected from a drop-down list.


Default: ""

</td>
</tr>
<tr>
<td valign="top">

ODBC Services

</td>
<td valign="top">

odbc service

</td>
<td valign="top">

array

</td>
<td valign="top">

An array of objects containing connection parameters for generic ODBC data sources such as databases. They can be used as ODBC data services in the project CCL. To be able to access them from the project CCL, the name of each object needs to match the corresponding service property in the project CCL. Each object contains reference to an ODBC DSN that needs to exist in the runtime environment. You can use com.sap.streaming Dockerfile to generate such DSN entries, as shown in an example in the bottom section of the Dockerfile.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Services File

</td>
<td valign="top">

services file

</td>
<td valign="top">

string

</td>
<td valign="top">

The location and name of the file generated by the operator, which contains all the data service entries available for use in the project CCL. Specifying this value may be useful for debugging issues with data service connectivity. If the value is left empty, the temporary file is used instead.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Log4j Properties

</td>
<td valign="top">

log4j properties

</td>
<td valign="top">

string

</td>
<td valign="top">

Specifies the log4j tracing properties that are used by the operator. By default, it includes output to console as well as to the logs/FlowAgent.log file at INFO trace level. You can change these settings individually.

Default: ""

</td>
</tr>
</table>



<a name="loio0b6100b9ce244d18ab709fe06227fe23__section_wth_pzm_k3b"/>

## Input

-   Any input port names must match an input stream or window in the project CCL. The operator publishes any incoming data rows to that input stream or window. Only string and message type ports are supported.

-   None.




<a name="loio0b6100b9ce244d18ab709fe06227fe23__section_vnj_rzm_k3b"/>

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

outError

</td>
<td valign="top">

string

</td>
<td valign="top">

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
<tr>
<td valign="top">

committedMessage

</td>
<td valign="top">

message

</td>
<td valign="top">

Notifies about commits of input messages. If mapped, for any input message that has a value specified for the `message.commit.token` header attribute the operator will emit an output message with an empty body and all header attributes from the original input message preserved. Before emitting this output message the operator will publish and commit all input rows contained in the corresponding input message.

</td>
</tr>
</table>

Any other output port names must match an output stream or window in the project CCL. The operator subscribes to that output stream or window for any outgoing data rows. Only string and message type ports are supported.



<a name="loio0b6100b9ce244d18ab709fe06227fe23__section_wll_szm_k3b"/>

## Functional Restrictions

The Streaming Analytics operator is based on streaming lite, which is a compact version of SAP HANA streaming analytics. The operator supports the following adapters:

-   All adapters built using the adapter toolkit. However, you can use only them in managed mode, which means the adapter starts and stops with the streaming analytics project.

-   The Streaming Web Output adapter is also supported.

-   Database Input and Output adapters.


Do not use the binaries or SDKs that come with the streaming install image to communicate with and send data to and from the streaming project. Instead, use the input and output ports on the operator, as well as any of the supported adapters.

There are additional functionalities and components that the operator does not support. These are based on the restrictions for streaming lite. For complete details, see the [Streaming Lite](https://help.sap.com/viewer/f1da0b944b1c4eae8137c9f913b66d44/2.0.04/en-US/6df3acf1ee9645418dff08f20c864a6a.html) section in the SAP HANA Streaming Analytics: Developer Guide. Keep these in mind as you use the Streaming Analytics operator and graphs.

For more information on building a streaming analytics project, see the [SAP HANA Streaming Analytics: Developer Guide](https://help.sap.com/viewer/f1da0b944b1c4eae8137c9f913b66d44/2.0.04/en-US) and [SAP HANA Streaming Analytics: CCL Reference](https://help.sap.com/viewer/608c361a786e4ec485224c890cbf1617/2.0.04/en-US).

