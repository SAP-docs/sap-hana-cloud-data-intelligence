<!-- loioe9b708d3aaa84b189a2b987b4f17fdf9 -->

# Azure SQL DB Table Consumer \(Deprecated\)

Reads from an Azure SQL Database table or view.



This operator is deprecated. We recommend using the [Table Consumer V2](table-consumer-v2-1e5f0ee.md) operator.

It uses Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator \(for example, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)\)



<a name="loioe9b708d3aaa84b189a2b987b4f17fdf9__section_sq1_nf3_vdb"/>

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

Azure SQL Database Connection

</td>
<td valign="top">

azuresqldbConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. The object containing the connection parameters to an Azure SQL Database.

</td>
</tr>
<tr>
<td valign="top">

Source Table

</td>
<td valign="top">

adapted\_dataset

</td>
<td valign="top">

object

</td>
<td valign="top">

Table from which the content will be read. It accepts two formats: adapted dataset of the target table, which can be selected via the table browsing action, or qualified name in `<Schema>.<TableName>` format.

</td>
</tr>
<tr>
<td valign="top">

Partition Type

</td>
<td valign="top">

partitionType

</td>
<td valign="top">

string

</td>
<td valign="top">

Partitioning used to enable data reading in parallel. In this case, the producer must be inside a group with multiplicity equal to the number of partitions \(**only** the producer, for example, Flowagent File Producer\).

Default: None

</td>
</tr>
<tr>
<td valign="top">

Logical Partition Specification

</td>
<td valign="top">

partitionSpecification

</td>
<td valign="top">

object

</td>
<td valign="top">

For more information, see [Partitioning](partitioning-86085d9.md).

</td>
</tr>
<tr>
<td valign="top">

Additional Session Parameters

</td>
<td valign="top">

additionalSessionParameters

</td>
<td valign="top">

string

</td>
<td valign="top">

Session parameters that affect the connection with the source.

</td>
</tr>
<tr>
<td valign="top">

Fetch Size

</td>
<td valign="top">

fetchSize

</td>
<td valign="top">

integer

</td>
<td valign="top">

The number of rows that will be fetched from the source in each request. For wide tables, smaller values are better. For tables with fewer columns, larger values are better.

Default: 100

</td>
</tr>
</table>



<a name="loioe9b708d3aaa84b189a2b987b4f17fdf9__section_knq_5f3_vdb"/>

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

`inTableName` 

</td>
<td valign="top">

string

</td>
<td valign="top">

SQL Server table name from which the data will be read, usually in `<Schema>.<TableName>` format.

> ### Note:  
> This is optional. It can be overridden by Source Table, so this port can also be used as a trigger.



</td>
</tr>
</table>



<a name="loioe9b708d3aaa84b189a2b987b4f17fdf9__section_swc_cg3_vdb"/>

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

`outConfig` 

</td>
<td valign="top">

string.flowagent.config

</td>
<td valign="top">

Flowagent type port, which only `Flowagent producers` can consume \(for example, Flowagent File Producer\). To get the data as string, `Flowagent CSV Producer`can be used as producer.

</td>
</tr>
<tr>
<td valign="top">

`outError` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Operator error. If mapped, the operator error is sent to the operator this port is mapped to and the graph remains running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

