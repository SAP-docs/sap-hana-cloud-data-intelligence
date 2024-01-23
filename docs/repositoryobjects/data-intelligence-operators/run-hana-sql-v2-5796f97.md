<!-- loio5796f97071ac44b386172f686fdaf015 -->

# Run HANA SQL V2

The Run HANA SQL operator executes user-provided SQL statements on an SAP HANA database.



<a name="loio5796f97071ac44b386172f686fdaf015__section_b3g_vnj_cjb"/>

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

Mode

</td>
<td valign="top">

mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines how the operator obtains the SQL code.

Accepted values:

-   *Static \(from configuration\)*: the operator executes the statement\(s\) specified in **SQL** and becomes idle.

-   *Dynamic \(from input\)*: the operator executes SQL statement\(s\) from each input message.


Default: "Dynamic \(from input\)"

</td>
</tr>
<tr>
<td valign="top">

SQL

</td>
<td valign="top">

sql

</td>
<td valign="top">

string

</td>
<td valign="top">

The SQL statement\(s\) to be executed when in *Static* mode. This value is ignored in Dynamic mode.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Decimal Output Format

</td>
<td valign="top">

decimalOutputFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines how the operator outputs the values for columns of type `DECIMAL` and `SMALLDECIMAL` in string format.

Accepted values:

-   `Fraction`: decimals are represented as string in `"<numerator>/<denominator>"` format \(for example, `"3/4"`\).

-   `Floating-point`: decimals are converted to double-precision floating-point numbers.

    > ### Note:  
    > The resulting number may not represent the exact value of the division as there can be a loss of precision.


Default: "Fraction"

</td>
</tr>
<tr>
<td valign="top">

CESU-8 Output Handling

</td>
<td valign="top">

cesu8Handling

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines how the operator deals with CESU-8 encoding problems. Such situation can happen due to the conversion from UTF-16 \(used in ABAP systems\) to CESU-8 or UTF-8 used internally to represent the values as strings.

This affects only character-based field types.

Accepted values:

-   **Default**: the operator throws an error describing the column and row that caused the problem.

    > ### Example:  
    > invalid CESU-8: <FIELD\_VALUE\> at pos: <POSITION\> row: 0 fieldname: <COLUMN\_NAME\>

-   **Replace**: incorrectly encoded CESU-8 chararcters are replaced with the Unicode replacement character \(`'\uFFFD'`\).
-   **Raw**: the data of all character-based columns is represented by the exact bytes stored in the database field with no transformation.

Default: "Default"

</td>
</tr>
<tr>
<td valign="top">

Transaction Level

</td>
<td valign="top">

transactionLevel

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines how the operator should group statements into database transactions.

Accepted values:

-   *Per input*: a separate transaction is used for each input, and each transaction encompasses all statements in that input. In *Static* mode, this means that the entire code in **SQL** is executed in a single transaction.

-   *Per statement*: a separate transaction is used for each statement, regardless of whether they came from the same input message.


Default: "Per input"

</td>
</tr>
<tr>
<td valign="top">

Batching

</td>
<td valign="top">

batching

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines how the operator output is sent in terms of batching.

Accepted values:

-   *None*: batching is not used.

-   *Fixed size*: output is sent in batches of fixed size \(specified in *Batch Size*\).

Default: "None"

</td>
</tr>
<tr>
<td valign="top">

Batch Size

</td>
<td valign="top">

batcheSize

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of rows to output in each batch. This parameter is used only when *Batching* is set to *Fixed size*, and it must be an integer greater than zero.

Default: 100

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



<a name="loio5796f97071ac44b386172f686fdaf015__section_d4d_5t3_cjb"/>

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

scalar

</td>
<td valign="top">

com.sap.core.string

</td>
<td valign="top">

A string containing SQL commands. This applies only to *Dynamic* mode.

</td>
</tr>
</table>



<a name="loio5796f97071ac44b386172f686fdaf015__section_krb_y1j_cjb"/>

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

\*

</td>
<td valign="top">

A dynamic table described in the header `com.sap.headers.hana.table` together with the retrieved data. For statements that do not query data, a table of type `com.sap.hana.affected` is sent containing the details of how many rows were affected. When statements execute DDL modifications, `affected` is sent as -1.

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

An error message, if applicable, as described at [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:.

</td>
</tr>
</table>



<a name="loio5796f97071ac44b386172f686fdaf015__section_hmw_lkb_pqb"/>

## State Management Support

State management support is provided when following configuration is used:

-   *Mode* set to *Static*;

-   *Transaction Level* set to *Per statement*;
-   *Batching* set to *Fixed size*.

The state is saved between statements, when there is more than one, and between batches, when there is data output. The operator offers *at-least-once guarantee* by saving the last statement executed and the batch index, when applicable. Upon recovery, the execution starts after the last statement saved and the data output starts from the last batch offset.

