<!-- loioba8d5ff099b34c53a496b5322c421c6e -->

# Redshift Table Consumer \(Deprecated\)

This operator reads from a Redshift table or view. It uses Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator.



This operator is deprecated. We recommend using the [Table Consumer V2](table-consumer-v2-1e5f0ee.md) operator.



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

Redshift Connection

</td>
<td valign="top">

redshiftConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. Object containing the connection parameters to a Redshift database.

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

Mandatory. Table from where the content is read. It accepts two formats: adapted dataset of the target table, which can be selected via the table browsing action, or qualified name in <Schema\>.<TableName\> format.

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

Partitioning is used to enable data reading in parallel. In this case, the **producer** must be inside a group with multiplicity equal to the number of partitions \(**only** the producer, for example, Flowagent File Producer\).

Default: ""

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

For more information about partitioning, check the [Logical Partitions](logical-partitions-83ccb1c.md) documentation.

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

Set session parameters that affect the connection with the source.

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

Indicates the number of rows fetched from the source in each request. For wide tables, smaller values are better. For tables with less columns, larger values are better.

Default: 1000

</td>
</tr>
</table>



<a name="loioba8d5ff099b34c53a496b5322c421c6e__section_rd1_rky_spb"/>

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

inTableName

</td>
<td valign="top">

string

</td>
<td valign="top">

SQL Server table name from which the data is read, usually in <Schema\>.<TableName\> format.

> ### Note:  
> Defining this port is optional. If `Source Table` is defined, then this port is ignored. Therefore, the input port can be used as a trigger.



</td>
</tr>
</table>



<a name="loioba8d5ff099b34c53a496b5322c421c6e__section_t3y_5ky_spb"/>

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

outConfig

</td>
<td valign="top">

string.flowagent.config

</td>
<td valign="top">

Flowagent type port, which only **Flowagent producers** can consume \(for example, [Flowagent File Producer \(Deprecated\)](flowagent-file-producer-deprecated-76e9d5c.md)\). In order to get the data as string, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md) can be used as producer.

</td>
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
</table>

