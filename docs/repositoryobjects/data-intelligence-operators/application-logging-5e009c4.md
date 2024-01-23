<!-- loio5e009c4c830841be9f281205de037077 -->

# Application Logging

The Application Logging operator for creating application logs.



It writes application messages as logs through the application logging API. It’s implemented in a way that it returns the request it receives as well as the output response from the application logging API.



<a name="loio5e009c4c830841be9f281205de037077__section_ed2_m5h_rrb"/>

## Configuring Process ID and Group ID

In order to create application logging for an operator, a process ID of the target operator must be provided. The group ID is optional.

1.  If the application logging operator is not directly connected to the target operator, the process ID must be provided in the configuration of the application logging operator.

    ```
    +---------+        +-----------+        +-------------+
    |         |-out--->|           |        | Application |
    |    T    |        | Converter |-out--->|   Logging   |
    |         |-error->|           |        |  Operator   |
    +---------+        +-----------+        +-------------+
    ```

2.  The process ID is optional, if the target operator is directly connected with the application logging operator.

    ```
    +---------+        +-------------+
    |         |        | Application |
    |    T    |-out--->|   Logging   |
    |         |        |  Operator   |
    +---------+        +-------------+
    ```

    > ### Note:  
    > To find out a process ID in a graph, select the operator and click on “Open Configuration”. The property `Id` in the configuration panel is the process ID.




<a name="loio5e009c4c830841be9f281205de037077__section_icq_w5h_rrb"/>

## Log Severity

The application logging supports the following severities:

```
"INFO", "WARNING", "ERROR"
```



<a name="loio5e009c4c830841be9f281205de037077__section_tkb_z5h_rrb"/>

## Message Format

The incoming message must follow the format below. It can be a single or an array of messages.

```
{
  text: "", // mandatory, log message
  severity: "", // optional, default "INFO"
  messageCode: "", // optional, e.g. "CR100400"
  details: {}, // optional, log details
  user: "" // optional
}
```



<a name="loio5e009c4c830841be9f281205de037077__section_gh2_bvh_rrb"/>

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

Graph Handle ID

</td>
<td valign="top">

graphId

</td>
<td valign="top">

string

</td>
<td valign="top">

The handle ID of the runtime graph which will be used for application logging. Optional, the graph handle ID is only needed if this operator is used in a subgraph to write application logs of its parent graph.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Process ID

</td>
<td valign="top">

operatorId

</td>
<td valign="top">

string

</td>
<td valign="top">

The process ID of the target operator which will be used for application logging. Optional, it’s only needed if the target operator is not directly connected to the application logging operator. See the Configuring Process ID and Group ID section.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Group ID

</td>
<td valign="top">

groupId

</td>
<td valign="top">

string

</td>
<td valign="top">

Optional. The ID of the group which contains the target operator.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Exit On Error

</td>
<td valign="top">

crashOnError

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Optional. Force to fail the application logging operator and exit the process with an exit code 1 if there is a message received at error port.

Default: false

</td>
</tr>
</table>



<a name="loio5e009c4c830841be9f281205de037077__section_pgf_5vh_rrb"/>

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

input

</td>
<td valign="top">

string

</td>
<td valign="top">

The received message \(a JSON-line string\) from the connected operator to create application logging. See the Message Format section.

</td>
</tr>
</table>



<a name="loio5e009c4c830841be9f281205de037077__section_f3j_yvh_rrb"/>

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

output

</td>
<td valign="top">

string

</td>
<td valign="top">

The output message contains a trigger event for the next operator that is connected to this port.

</td>
</tr>
<tr>
<td valign="top">

error

</td>
<td valign="top">

message.error

</td>
<td valign="top">

The error output message contains a trigger event and an error message for the next operator that is connected to this port.

</td>
</tr>
</table>

Both output ports write the following example message \(JSON-line string\):

```
'{"event":"trigger","data":{"logMessages":[{"details":"log details","messageCode":"100030","severity":"INFO","user":"username","text":"log message"}],"message":"application logging operator execution message"}}'
```

> ### Note:  
> Leaving the error port unconnected will cause a graph failure, if there is a message received at this port.

