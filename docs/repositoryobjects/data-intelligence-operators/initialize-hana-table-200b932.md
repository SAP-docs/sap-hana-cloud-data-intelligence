<!-- loio200b93216122492e98b1e0a261c5bb7e -->

# Initialize HANA Table

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

-   *Dynamic \(from input\)*: The operator uses each input message to determine the name, columns, and primary key of the target table. These are obtained from the standard attributes in a [Table Messages](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/cf6b74cc9e974981b5bd7400a131ebec.html "A table message is an SAP Data Intelligence Modeler message that represents tabular data. The port type for table messages is message.table.") :arrow_upper_right:.


Default: " "

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

-   **Truncate** or **Delete**: it compares the existing table to the configured one. If there are no inconsistencies, it empties the table using a `TRUNCATE` or `DELETE` statement. Otherwise, an error is thrown.

-   **Drop \(Restrict\)**: it drops and re-creates the table using a `DROP (...) RESTRICT` statement.

-   **Drop \(Cascade\)**: it drops and re-creates the table using a `DROP (...) CASCADE` statement.


Default: "Create"

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
</table>



<a name="loio200b93216122492e98b1e0a261c5bb7e__section_d4d_5t3_cjb"/>

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

input

</td>
<td valign="top">

message.table

</td>
<td valign="top">

A [Table Messages](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/cf6b74cc9e974981b5bd7400a131ebec.html "A table message is an SAP Data Intelligence Modeler message that represents tabular data. The port type for table messages is message.table.") :arrow_upper_right: that specifies which table is initialized. This only applies to **Dynamic** mode.

The operator uses the following values from the input:

-   `Name` \(`Attributes.table.name`\)

-   `Columns` \(`Attributes.table.columns`\)

-   `Primary key` \(`Attributes.table.primaryKey`\)




</td>
</tr>
</table>



<a name="loio200b93216122492e98b1e0a261c5bb7e__section_krb_y1j_cjb"/>

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

success

</td>
<td valign="top">

message.table

</td>
<td valign="top">

A [Table Messages](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/cf6b74cc9e974981b5bd7400a131ebec.html "A table message is an SAP Data Intelligence Modeler message that represents tabular data. The port type for table messages is message.table.") :arrow_upper_right: describing the table that was successfully initialized.

In **Dynamic** mode, this output also includes any additional attributes that were present in the input, as well as the original message body.

</td>
</tr>
<tr>
<td valign="top">

error

</td>
<td valign="top">

message.error

</td>
<td valign="top">

An Error Message, in case an error was raised during an operation.

</td>
</tr>
</table>

