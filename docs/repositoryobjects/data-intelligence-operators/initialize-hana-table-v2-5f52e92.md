<!-- loio5f52e921972e49789fc81f9653c534bf -->

# Initialize HANA Table V2

The Initialize HANA Table operator can initialize one or more tables on an SAP HANA database.



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

Determines how the operator obtains the values for the table name, column specification, and primary key.

Accepted values:

-   *Static \(from configuration\)*: The operator does not expect any input. It initializes a table based on the configuration properties `Table name`, `Table columns`, and `Primary key`. It initializes the table as soon as it starts running, writes the relevant output, and becomes idle.

-   *Dynamic \(from input\)*: The operator uses each input message to determine the name, columns, and primary key of the target table. These are obtained from the header `com.sap.headers.hana.table` as explained in the [Input](initialize-hana-table-v2-5f52e92.md#loio5f52e921972e49789fc81f9653c534bf__section_d4d_5t3_cjb) section below.


Default: "Dynamic \(from input\)"

</td>
</tr>
<tr>
<td valign="top">

Initialization Mode

</td>
<td valign="top">

initMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines how the operator should initialize the table\(s\).

If the table does not yet exist, the operator only creates it.

If the table already exists:

-   **Create**: it compares the existing table to the configured or received one. If there are inconsistencies, an error is thrown.

-   **Truncate** or **Delete**: it compares the existing table to the confiured or received one. If there are inconsistencies, it empties the table using `TRUNCATE` or `DELETE` statement. Otherwise, an error is thrown.

-   **Drop \(Restrict\)**: it drops and re-creates the table using a `DROP (...) RESTRICT` statement.

-   **Drop \(Cascade\)**: it drops and re-creates the table using a `DROP (...) CASCADE` statement.


Default: "Create"

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

The name of the table that is initialized in `Static` mode.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Table Columns

</td>
<td valign="top">

tableColumns

</td>
<td valign="top">

array

</td>
<td valign="top">

The list of columns that are used, in `Static` mode, if the table needs to be created. This is used only when the table does not yet exist or `Initialization mode` is set to either `Drop` option.

Default: \[\]

</td>
</tr>
<tr>
<td valign="top">

Primary Key

</td>
<td valign="top">

primaryKey

</td>
<td valign="top">

array

</td>
<td valign="top">

A list of column names to be used as a primary key in `Static` mode.

Default: \[\]

</td>
</tr>
<tr>
<td valign="top">

Table Type

</td>
<td valign="top">

tableType

</td>
<td valign="top">

string

</td>
<td valign="top">

The type of table that is created.

Accepted values:

-   Row

-   Column


Default: "Row"

</td>
</tr>
<tr>
<td valign="top">

Output Initialized Table

</td>
<td valign="top">

outputInitializedTable

</td>
<td valign="top">

bool

</td>
<td valign="top">

Controls whether the table to be created when in `Static` mode should be sent via the output port.

Default: false

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

The maximum amount of time to wait for the server. If at any time the operator does not hear from the server within this period of time, the connection is closed. If set to zero, the operator waits for the server indefinitely.

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



<a name="loio5f52e921972e49789fc81f9653c534bf__section_d4d_5t3_cjb"/>

## Input


<table>
<tr>
<th valign="top">

Input

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

A dynamic table containing the `com.sap.headers.hana.table` header with complete DDL details that specifies the table to be initialized. This is only applicable in `Dynamic` mode. In `Static` mode, the inputs are simply forwarded to the next operator when the table defined in the configurations has been initialized.

</td>
</tr>
</table>



<a name="loio5f52e921972e49789fc81f9653c534bf__section_krb_y1j_cjb"/>

## Output


<table>
<tr>
<th valign="top">

Output

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

A dynamic table with the header `com.sap.headers.hana.table` describing the table that was successfully initialized, with an empty body. In `Static` mode, the first output will be the initialized table, if `Output Initialized Table` is set to `true`. Any additional output will be a copy of the inputs received as explained above.

</td>
</tr>
</table>

