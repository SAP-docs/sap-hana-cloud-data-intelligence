<!-- loio4bbba4b047b44986af3acb30e82cc3df -->

# DB2 SQL Consumer \(Deprecated\)

Performs a SQL query in a DB2 database.



This operator is deprecated. We recommend using the [SQL Consumer V2](sql-consumer-v2-a4a74c3.md) operator.

It uses Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator \(for example, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)\).



<a name="loio4bbba4b047b44986af3acb30e82cc3df__section_hgl_2p2_p2b"/>

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

DB2 Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a DB2 database.

</td>
</tr>
<tr>
<td valign="top">

Native SQL

</td>
<td valign="top">

string

</td>
<td valign="top">

SQL statement that will be used to read from the source. The syntax depends on the underlying source.

</td>
</tr>
<tr>
<td valign="top">

Additional Session Parameters

</td>
<td valign="top">

string

</td>
<td valign="top">

Set session parameters that will affect the connection with the source.

</td>
</tr>
<tr>
<td valign="top">

Partition Type

</td>
<td valign="top">

string

</td>
<td valign="top">

Partitioning is used to enable data reading in parallel. In this case, the producer must be inside a group with multiplicity equal to the number of partitions \(only the producer, for example, Flowagent File Producer\).

Default: None

</td>
</tr>
<tr>
<td valign="top">

Logical Partition Specification

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

Fetch Size

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the number of rows that will be fetched from the source in each request. For wide tables, smaller values are better. For tables with fewer columns, larger values are better.

Default: 100

</td>
</tr>
</table>



<a name="loio4bbba4b047b44986af3acb30e82cc3df__section_jgl_2p2_p2b"/>

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

`inSQL` 

</td>
<td valign="top">

string

</td>
<td valign="top">

SQL statement that will be used to read from the source. The syntax depends on the underlying source.

> ### Note:  
> This is optional. It can be overridden by Native SQL, so this port can also be used as a trigger.



</td>
</tr>
</table>



<a name="loio4bbba4b047b44986af3acb30e82cc3df__section_lgl_2p2_p2b"/>

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

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

