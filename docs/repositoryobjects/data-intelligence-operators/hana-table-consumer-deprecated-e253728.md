<!-- loioe253728ecd7f448bac1755f3f67a140e -->

# HANA Table Consumer \(Deprecated\)

The HANA Table Consumer reads from a HANA table or view.



It uses the Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator \(for example, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)\).



<a name="loioe253728ecd7f448bac1755f3f67a140e__section_ely_qnp_lhb"/>

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

HANA Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a HANA database.

</td>
</tr>
<tr>
<td valign="top">

Source Table

</td>
<td valign="top">

string

</td>
<td valign="top">

HANA table name

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

Fetch Size

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the number of rows that will be fetched from the source in each request. For wide tables, smaller values are better; for tables with few columns, larger values are better.

Default: 100

</td>
</tr>
</table>



<a name="loioe253728ecd7f448bac1755f3f67a140e__section_gly_qnp_lhb"/>

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

Table name from which the data will be read, usually in `<Schema>.<TableName>` format.

> ### Note:  
> This is optional. It can be overridden by Source Table, so this port can also be used as a trigger.



</td>
</tr>
</table>



<a name="loioe253728ecd7f448bac1755f3f67a140e__section_ily_qnp_lhb"/>

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

