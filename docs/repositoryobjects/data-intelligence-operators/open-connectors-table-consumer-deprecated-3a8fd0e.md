<!-- loio3a8fd0e38cd94bb5a4973177212a2b22 -->

# Open Connectors Table Consumer \(Deprecated\)

Open Connectors Table Consumer gets all data from the given table name from SAP BTP Open Connectors.



This operator is deprecated. We recommend using the [SAP Application Consumer V2](sap-application-consumer-v2-7a1527d.md) operator.

It uses the Flowagent subengine for execution \(for example, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)\).



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

Open Connectors Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Connection parameters or connection ID of an Open Connectors connection in Connection Management.

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

Source table name in an `SAP BTP Open Connectors` instance. It's also called `object name` in Open Connectors.

</td>
</tr>
<tr>
<td valign="top">

Access Method

</td>
<td valign="top">

string

</td>
<td valign="top">

Open Connectors API used for retrieving data. In GET mode, Open Connectors' data query API is called directly once per page to retrieve data. In `BULK` method, an asynchronous query jobis created at Open Connectors and then start streaming data.

Default: GET

</td>
</tr>
</table>



<a name="loio3a8fd0e38cd94bb5a4973177212a2b22__section_i2l_n2s_fhb"/>

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

Source table name in an `SAP BTP Open Connectors` instance. It is also called object name in Open Connectors.

</td>
</tr>
</table>

**Data Type Mapping**


<table>
<tr>
<th valign="top">

Open Connection Type

</th>
<th valign="top">

Vendor Native Type

</th>
<th valign="top">

SAP Data Intelligence Type

</th>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">



</td>
<td valign="top">

NVARCHAR\(5000\)

</td>
</tr>
<tr>
<td valign="top">

numeric

</td>
<td valign="top">

int

</td>
<td valign="top">

INTEGER

</td>
</tr>
<tr>
<td valign="top">

numeric

</td>
<td valign="top">



</td>
<td valign="top">

FLOATING\(8\)

</td>
</tr>
<tr>
<td valign="top">

boolean

</td>
<td valign="top">



</td>
<td valign="top">

INTEGER

</td>
</tr>
<tr>
<td valign="top">

date

</td>
<td valign="top">

date

</td>
<td valign="top">

DATE

</td>
</tr>
<tr>
<td valign="top">

date

</td>
<td valign="top">

datetime

</td>
<td valign="top">

DATETIME

</td>
</tr>
<tr>
<td valign="top">

object

</td>
<td valign="top">



</td>
<td valign="top">

NVARCHAR\(5000\)

</td>
</tr>
</table>



<a name="loio3a8fd0e38cd94bb5a4973177212a2b22__section_itx_3gs_fhb"/>

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

Flowagent type port, which only Flowagent producers can consume \(for example, `Flowagent File Producer`\). To get the data as string, `Flowagent CSV Producer` can be used as producer.

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

