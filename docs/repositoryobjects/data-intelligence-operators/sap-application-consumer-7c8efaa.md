<!-- loio7c8efaaef20e44b6a3d40fa23f4e68bf -->

# SAP Application Consumer

Use the SAP Application Consumer operator to consume data from SAP and non-SAP sources as modeled in a graph. Supported in Generation 1 graphs.



This operator reads from a variety of SAP and non-SAP applications. The operator produces structured output, and you need to connect it to other operators from the Structured Operators category. For example, [Data Transform V2](data-transform-v2-a415f61.md) or [Structured File Producer V3](structured-file-producer-v3-605e08a.md).

This operator uses a custom editor user interface.



<a name="loio7c8efaaef20e44b6a3d40fa23f4e68bf__section_qmh_nl5_fnb"/>

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

Service

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

Connection ID

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

Source

</td>
<td valign="top">

Object

</td>
<td valign="top">

Remote dataset of the selected source object.

</td>
</tr>
<tr>
<td valign="top">

Trace level

</td>
<td valign="top">

String

</td>
<td valign="top">

Trace level of the extraction.

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

Maximum Fetch Size

</td>
<td valign="top">

Integer

</td>
<td valign="top">

The maximum number of records from the source included in each batch. The actual number of records is automatically calculated based on the dataset definition. To disable the automatic calculation, set the *Use Defined Fetch Size* option to *True*.

</td>
</tr>
<tr>
<td valign="top">

Use Defined Fetch Size

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Set to *True* when the automatic calculation doesn’t provide optimal performance. When set to *True*, each batch of records contains the number of records entered in the *Maximum Fetch Size* option. For example, when *Maximum Fetch Size* is set to 1000, and *Use Defined Fetch Size* is set to *True*, then there are 1000 records in each batch. When set to *False*, then each batch is between 10 and 1000 rows.

</td>
</tr>
<tr>
<td valign="top">

Access Method

</td>
<td valign="top">

String

</td>
<td valign="top">

Open Connectors API used for retrieving data. In *GET* mode, Open Connectors’ data query API is called directly once per page to retrieve data. In *BULK* method, an asynchronous query job is created at Open Connectors and then starts streaming data.

</td>
</tr>
</table>



<a name="loio7c8efaaef20e44b6a3d40fa23f4e68bf__section_pty_hm5_fnb"/>

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



<a name="loio7c8efaaef20e44b6a3d40fa23f4e68bf__section_p31_rm5_fnb"/>

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

**Related Information**  


[Custom Editor](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/8cda7c3a4ab74c86ba5752456418c4b0.html "Use the Custom Editor to update the source dataset and projection and filters are pushed down to the source.") :arrow_upper_right:

