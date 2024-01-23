<!-- loiob6a5c17fafcb47efa4b2baa030dcc307 -->

# Write HANA Table V2

The Write HANA Table operator ingests data into one or more tables on an SAP HANA database.



The target table\(s\) must already exist at initialization time \(in *Static* mode\) or whenever input is received \(in *Dynamic* mode\). If table creation is intended as part of the same pipeline, consider using the [Initialize HANA Table V2](initialize-hana-table-v2-5f52e92.md) operator in conjunction with this one.



<a name="loiob6a5c17fafcb47efa4b2baa030dcc307__section_ml2_3xj_cjb"/>

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

Connection

</td>
<td valign="top">

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. The object containing the connection parameters to a HANA instance.

Default: \{\}

</td>
</tr>
<tr>
<td valign="top">

Configuration Mode

</td>
<td valign="top">

configMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines how the operator obtains the target table name.

Accepted values:

-   *Static \(from configuration\)*: The operator ingests all incoming data into the table specified in *Table Name*.

-   *Dynamic \(from input\)*: The operator uses each input message to determine the destination.


Default: "Dynamic \(from input\)"

</td>
</tr>
<tr>
<td valign="top">

Table Name

</td>
<td valign="top">

tableName

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the table to be used as fixed destination in *Static* mode.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Statement Type

</td>
<td valign="top">

statementType

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines whether data is to be ingested using an `INSERT` or an `UPSERT` statement.

Default: "INSERT"

</td>
</tr>
<tr>
<td valign="top">

Connection Timeout

</td>
<td valign="top">

connectionTimeout

</td>
<td valign="top">

string

</td>
<td valign="top">

The maximum amount of time to wait for the server. If the operator does not hear from the server within this period of time, the connection is closed. If set to zero, the operator waits for the server indefinitely.

Default: "50s"

</td>
</tr>
<tr>
<td valign="top">

Error Handling

</td>
<td valign="top">

errorHandling

</td>
<td valign="top">

string

</td>
<td valign="top">

Details available at [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:.

Default: "terminate on error"

</td>
</tr>
</table>



<a name="loiob6a5c17fafcb47efa4b2baa030dcc307__section_d4d_5t3_cjb"/>

## Input


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Kind

</th>
<th valign="top">

Type ID

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

input

</td>
<td valign="top">

table

</td>
<td valign="top">

\*

</td>
<td valign="top">

It depends on the *Configuration Mode*:

-   **Dynamic \(from input\)**: A dynamic table containing the `com.sap.headers.hana.table` header with complete DDL details, or at least the table name, as well as the data to be inserted.

-   **Static \(from configuration\)**: A dynamic table with the data to be inserted.

The `com.sap.headers.hana.table` header with complete DDL details is not necessary in this case but is taken into account if provided \(except for the table name\).

</td>
</tr>
</table>



<a name="loiob6a5c17fafcb47efa4b2baa030dcc307__section_krb_y1j_cjb"/>

## Output


<table>
<tr>
<th valign="top">

Output

</th>
<th valign="top">

Kind

</th>
<th valign="top">

Type ID

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

success

</td>
<td valign="top">

table

</td>
<td valign="top">

com.sap.hana.affected

</td>
<td valign="top">

A table of type `com.sap.hana.affected` containing the details of how many rows were received and affected. The output also includes the header `com.sap.headers.hana.table` with details of the table and columns that were modified by the input and data received. Due to a limitation on the HANA driver side, it is not possible to keep track of the affected rows when there are LOB columns involved, so the output will contain a -1 for it instead.

</td>
</tr>
<tr>
<td valign="top">

error

</td>
<td valign="top">

structure

</td>
<td valign="top">

com.sap.error

</td>
<td valign="top">

An error message, if applicable \(see [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:\).

</td>
</tr>
</table>

