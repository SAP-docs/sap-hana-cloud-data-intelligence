<!-- loio4b570d42344f46a0913576e8a885d1ab -->

# SQL Server SQL Consumer \(Deprecated\)

The SQL Server SQL Consumer performs an SQL query in an SQL Server database.



This operator is deprecated. We recommend using the [SQL Consumer V2](sql-consumer-v2-a4a74c3.md) operator.

It uses the Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator \(for example, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)\).



<a name="loio4b570d42344f46a0913576e8a885d1ab__section_sq1_nf3_vdb"/>

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

SQL Server Connection

</td>
<td valign="top">

microsoftsqlserverConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a MySQL database.

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

SQL statement used to read from the source. The syntax depends on the underlying source.

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



<a name="loio4b570d42344f46a0913576e8a885d1ab__section_knq_5f3_vdb"/>

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

SQL statement used to read from the source. The syntax depends on the underlying source.

> ### Note:  
> This is optional. It can be overridden by Native SQL, so this port can also be used as a trigger.



</td>
</tr>
</table>



<a name="loio4b570d42344f46a0913576e8a885d1ab__section_swc_cg3_vdb"/>

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

Operator error. If mapped, the operator error is sent to the operator this port is mapped to and the graph remains running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

