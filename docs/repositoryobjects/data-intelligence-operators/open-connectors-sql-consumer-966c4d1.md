<!-- loio966c4d1858364994b520a19c9808b79c -->

# Open Connectors SQL Consumer

The Open Connectors SQL Consumer gets and filters data by the given SQL statement from SAP BTP Open Connectors.



It uses the Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator \(for example, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)\).



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

Access Method

</td>
<td valign="top">

string

</td>
<td valign="top">

Open Connectors API used for retrieving data. In `GET` mode, Open Connectors' data query API is called directly once per page to retrieve data. In `BULK` method, an asynchronous query job is created at Open Connectors and then start streaming data.

Default: GET

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

SQL statement that is used to read and filter data from the source.

</td>
</tr>
</table>



<a name="loio966c4d1858364994b520a19c9808b79c__section_id2_33s_fhb"/>

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

SQL statement that is used to read and filter data from the source. Supported SQL syntax is limited as follows:

```
SELECT <field-list> FROM <tableName> [WHERE <where-clause>] [ORDER BY <order-by-clause>]
```

-   field-list = `* | field1, field2, ...`
-   where-clause = `WHERE` expression `AND/OR` expression `AND/OR` ...
-   order-by-clause = `field1 asc/desc` \(only allow one field\)
-   expression = field `operator` value



</td>
</tr>
</table>



### Valid Operators


<table>
<tr>
<th valign="top">

Operator

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

=

</td>
<td valign="top">

Equal to

</td>
</tr>
<tr>
<td valign="top">

!=

</td>
<td valign="top">

Not equal to

</td>
</tr>
<tr>
<td valign="top">

<

</td>
<td valign="top">

Less than

</td>
</tr>
<tr>
<td valign="top">

\>

</td>
<td valign="top">

Greater than

</td>
</tr>
<tr>
<td valign="top">

<=

</td>
<td valign="top">

Less than or equal to

</td>
</tr>
<tr>
<td valign="top">

\>=

</td>
<td valign="top">

Greater than or equal to

</td>
</tr>
<tr>
<td valign="top">

LIKE

</td>
<td valign="top">

TRUE if the operand matches a pattern

</td>
</tr>
<tr>
<td valign="top">

IN

</td>
<td valign="top">

TRUE if the operand is equal to one of a list of expressions

</td>
</tr>
<tr>
<td valign="top">

IS NULL

</td>
<td valign="top">

TRUE if a NULL value is found

</td>
</tr>
</table>



### Data Type Mapping

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



<a name="loio966c4d1858364994b520a19c9808b79c__section_itx_3gs_fhb"/>

## Output

****


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

