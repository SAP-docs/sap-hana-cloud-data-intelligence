<!-- loio39e91a157c56450ebed1c0dcdc717803 -->

# SAP Application Consumer V1 \(Deprecated\)

Use the SAP Application Consumer operator to consume data from SAP and non-SAP sources as modeled in a graph. Previously supported in Generation 1 graphs.



This operator reads from a variety of SAP and non-SAP applications. The operator produces structured output, and you need to connect it to other operators from the Structured Operators category. For example, [Data Transform V2](data-transform-v2-a415f61.md) or [Structured File Producer V3](structured-file-producer-v3-605e08a.md).

This operator uses a custom editor user interface.



<a name="loio39e91a157c56450ebed1c0dcdc717803__section_qmh_nl5_fnb"/>

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

Application Type

</td>
<td valign="top">

String

</td>
<td valign="top">

The application from where to consume tabular data.

</td>
</tr>
<tr>
<td valign="top">

oData Connection

</td>
<td valign="top">

Object

</td>
<td valign="top">

Connection ID of the source system.

</td>
</tr>
<tr>
<td valign="top">

oData Dataset

</td>
<td valign="top">

Object

</td>
<td valign="top">

OData Entity Set object.

</td>
</tr>
<tr>
<td valign="top">

Cloud Data Integration Connection

</td>
<td valign="top">

Object

</td>
<td valign="top">

Connection ID of the source system.

</td>
</tr>
<tr>
<td valign="top">

Cloud Data Integration Dataset

</td>
<td valign="top">

Object

</td>
<td valign="top">

Cloud Data Integration source dataset.

</td>
</tr>
<tr>
<td valign="top">

Default \(N\)VARCHAR Size

</td>
<td valign="top">

String

</td>
<td valign="top">

The default size of a varchar. The valid range is 0–5000.

</td>
</tr>
<tr>
<td valign="top">

Batch Query

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Determines whether the query is performed in batches. When true, the query to the OData source is performed batch by batch. Each batch is the size specified in *Fetch Size*.

</td>
</tr>
<tr>
<td valign="top">

Fetch Size

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Indicates the number of rows fetched from the source in each request. For wide tables, smaller values are better. For tables with less columns, larger values are better.

</td>
</tr>
</table>



<a name="loio39e91a157c56450ebed1c0dcdc717803__section_pty_hm5_fnb"/>

## Input


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

inTrigger

</td>
<td valign="top">

message

</td>
<td valign="top">

Trigger to indicate that the operator should start processing.

> ### Note:  
> The input port is optional. If the input port does not have a connection, then the operator starts when the graph starts running.



</td>
</tr>
</table>



<a name="loio39e91a157c56450ebed1c0dcdc717803__section_p31_rm5_fnb"/>

## Output


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

outTable

</td>
<td valign="top">

table

</td>
<td valign="top">

Table type port, which can be used to connect to other structured operators.

</td>
</tr>
</table>

