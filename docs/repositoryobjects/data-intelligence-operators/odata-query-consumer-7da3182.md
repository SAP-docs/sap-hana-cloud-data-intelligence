<!-- loio7da318268ecb46b6acd82e5c879514dd -->

# OData Query Consumer

The OData Query Consumer reads from an OData RESTful API.



It uses Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator \(for example, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)\).



<a name="loio7da318268ecb46b6acd82e5c879514dd__section_sq1_nf3_vdb"/>

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

OData Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to OData.

</td>
</tr>
<tr>
<td valign="top">

Default `(N)VARCHAR` Size

</td>
<td valign="top">

integer

</td>
<td valign="top">

The default size of a `varchar`.

Default: 1024

</td>
</tr>
<tr>
<td valign="top">

Batch Query

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Whether the query is performed in batches or not.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Query

</td>
<td valign="top">

string

</td>
<td valign="top">

OData Query Uniform Resource Indicator \(URI\) that is standard to this OData source.

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



<a name="loio7da318268ecb46b6acd82e5c879514dd__section_knq_5f3_vdb"/>

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

OData Query URI that is valid for this OData Source.

> ### Note:  
> This is optional. If Query is presented, this port is ignored.



</td>
</tr>
</table>



<a name="loio7da318268ecb46b6acd82e5c879514dd__section_swc_cg3_vdb"/>

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

FlowAgent type port, which only `Flowagent producers` can consume \(for example, Flowagent File Producer\). To get the data as string, `Flowagent CSV Producer` can be used as producer.

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

