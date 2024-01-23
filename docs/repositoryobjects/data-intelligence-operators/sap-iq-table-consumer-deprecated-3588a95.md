<!-- loio3588a953607a450fa16305ed4191c9b6 -->

# SAP IQ Table Consumer \(Deprecated\)

The SAP IQ Table Consumer reads from an SAP IQ table or view.



This operator is deprecated. We recommend using the [Table Consumer V2](table-consumer-v2-1e5f0ee.md) operator.

It uses the Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator \(for example, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)\).



<a name="loio3588a953607a450fa16305ed4191c9b6__section_sq1_nf3_vdb"/>

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

SAP IQ Connection

</td>
<td valign="top">

sapiqConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. The object containing the connection parameters to an SAP IQ database.

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

Mandatory. Table from which the content will be read. It accepts two formats: adapted dataset of the target table, which can be selected via the table browsing action, or qualified name in <Schema\>.<TableName\> format.

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

Partitioning is used to enable data reading in parallel. In this case, the producer must be inside a group with multiplicity equal to the number of partitions \(**only** the producer, for eample, Flowagent File Producer\).

Default: "None"

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

Set session parameters, which will affect the connection with the source.

Default: ""

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

Indicates the number of rows that will be fetched from the source in each request. For wide tables, smaller values are better. For tables with fewer columns, larger values are better.

Default: 1000

</td>
</tr>
</table>



<a name="loio3588a953607a450fa16305ed4191c9b6__section_knq_5f3_vdb"/>

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

SQL Server table name from which the data is read, usually in `<Schema>.<Tablename>` format.

> ### Note:  
> Defining this port is optional. If `Source Table` is defined, then this port is ignored. Therefore, the input port can be used as a trigger.



</td>
</tr>
</table>



<a name="loio3588a953607a450fa16305ed4191c9b6__section_swc_cg3_vdb"/>

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

Flowagent type port, which only Flowagent producers can consume \(for example, Flowagent File Producer\). To get the data as string, Flowagent CSV Producer can be used as producer.

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

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

