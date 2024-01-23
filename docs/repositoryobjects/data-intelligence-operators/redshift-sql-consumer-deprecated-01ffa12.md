<!-- loio01ffa12d2f524e9499b667a7f92e8e79 -->

# Redshift SQL Consumer \(Deprecated\)

This operator performs a SQL Query in a Redshift database. It uses Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator.



This operator is deprecated. We recommend using the [SQL Consumer V2](sql-consumer-v2-a4a74c3.md) operator.



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

Native SQL

</td>
<td valign="top">

native\_sql\_statement

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. SQL statement used to read from the source. The syntax depends on the underlying source.

Default: ""

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

For more information about partitioning, check the [Logical Partitions](logical-partitions-83ccb1c.md) documentation.

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



<a name="loio01ffa12d2f524e9499b667a7f92e8e79__section_eyw_1jy_spb"/>

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

inSQL

</td>
<td valign="top">

string

</td>
<td valign="top">

SQL statement used to read from the source. The syntax depends on the underlying source.

> ### Note:  
> this is optional. It can be overriden by `Native SQL`, so this port can also be used as a trigger.



</td>
</tr>
</table>



<a name="loio01ffa12d2f524e9499b667a7f92e8e79__section_uzm_jjy_spb"/>

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

