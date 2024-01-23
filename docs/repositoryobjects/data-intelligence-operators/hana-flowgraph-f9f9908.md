<!-- loiof9f9908f4830489695a61ef6e421ffe2 -->

# HANA Flowgraph

The HANA flowgraph operator helps execute an SAP HANA flowgraph in an SAP HANA system.



Executing an HANA flowgraph operator within a graph helps you to transform data from a remote source into SAP HANA either in batch or real-time mode. The flowgraphs are predefined in the server and represents a complete data flow. User must select the required SAP HANA flowgraph, and all the operations that the flowgraph must perform is defined in the server.



This operator has one input port \(`input`\) and two output ports \(`output` and `error`\). Use this operator in a graph that uses only other data workflow operators.

Connect the input port to another data workflow operator to trigger its start. On the `error` output port, the engine writes a message in case of errors when trying to execute the flowgraph. On success, the engine writes a message on the `output` port. If you want the execution of the graph to proceed, connect the respective output ports to other data workflow operators.

> ### Note:  
> Any message written to an unconnected output port results in the graph failure.



<a name="loiof9f9908f4830489695a61ef6e421ffe2__section_sq1_nf3_vdb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Parameter

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

SAP HANA Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Connection ID that references a connection to an SAP HANA system.

</td>
</tr>
<tr>
<td valign="top">

SAP HANA Flowgraph Name

</td>
<td valign="top">

string

</td>
<td valign="top">

Fully qualified SAP HANA Flowgraph name including schema name. For example, `/FLOWGRAPH_SCHEMA/PACKAGE::NAME`

</td>
</tr>
<tr>
<td valign="top">

Variables

</td>
<td valign="top">

array

</td>
<td valign="top">

Name-value pairs for substitution parameters. The default value is no variables.

</td>
</tr>
<tr>
<td valign="top">

Table Variables

</td>
<td valign="top">

array

</td>
<td valign="top">

Fully quoted SAP HANA table or view names. The default value is no variables.

</td>
</tr>
<tr>
<td valign="top">

Retry Interval

</td>
<td valign="top">

string

</td>
<td valign="top">

Time interval in seconds \(default 20\) to wait until next status update.

</td>
</tr>
<tr>
<td valign="top">

Retry Attempts

</td>
<td valign="top">

string

</td>
<td valign="top">

Maximum number of attempts \(default 10\) to query for status update.

</td>
</tr>
</table>



<a name="loiof9f9908f4830489695a61ef6e421ffe2__section_knq_5f3_vdb"/>

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

`input` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Accepts message from a connected data workflow operator.

</td>
</tr>
</table>



<a name="loiof9f9908f4830489695a61ef6e421ffe2__section_swc_cg3_vdb"/>

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

`output` 

</td>
<td valign="top">

string

</td>
<td valign="top">

If the operator executed successfully, this port carries the success message.

</td>
</tr>
<tr>
<td valign="top">

`error` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Operator error. If the port is connected, then the graph will keep running. If it is not connected, the graph will terminate with the operator error.

</td>
</tr>
</table>



For more information on how to use this operator, see [Run a HANA Flowgraph Operator](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/429c135ef23842b5a6d303914b8febae.html "To run (execute) an SAP HANA Flowgraph in an SAP HANA system, use the HANA flowgraph operator in the SAP Data Intelligence Modeler application.") :arrow_upper_right:.

