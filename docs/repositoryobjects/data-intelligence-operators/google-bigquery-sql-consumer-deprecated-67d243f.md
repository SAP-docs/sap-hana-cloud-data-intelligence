<!-- loio67d243f60ccc4ac980bf3bd3160d3269 -->

# Google BigQuery SQL Consumer \(Deprecated\)

Performs a SQL query to a Google BigQuery table.



This operator is deprecated. We recommend using the [SQL Consumer V2](sql-consumer-v2-a4a74c3.md) operator.

It uses the Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator \(for example, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)\).



<a name="loio67d243f60ccc4ac980bf3bd3160d3269__section_hgl_2p2_p2b"/>

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

Google BigQuery Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a Google BigQuery database.

</td>
</tr>
<tr>
<td valign="top">

BigQuery SQL

</td>
<td valign="top">

string

</td>
<td valign="top">

SQL statement that will be used to read from the source. Only syntax of BigQuery SQL \(legacy SQL\) is supported.

</td>
</tr>
</table>



<a name="loio67d243f60ccc4ac980bf3bd3160d3269__section_jgl_2p2_p2b"/>

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

SQL statement that is used to read from the source. The syntax depends on the underlying source.

> ### Note:  
> This is optional. If BigQuery SQL is presented, this port is ignored.



</td>
</tr>
</table>



<a name="loio67d243f60ccc4ac980bf3bd3160d3269__section_lgl_2p2_p2b"/>

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

Flowagent type port, which only `Flowagent producers` can consume \(for example, Flowagent File Producer\).

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

