<!-- loiob51adedc86404c79afda7bbca3b958aa -->

# Read HANA Table V2

The Read HANA Table operator reads data from a table in SAP HANA.



<a name="loiob51adedc86404c79afda7bbca3b958aa__section_b3g_vnj_cjb"/>

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

Specifies how the operator determines the table \(and which of its columns\) to be read.

Accepted values:

-   *Static \(from configuration\)*: the operator does not expect any input. It reads from the table identified in*Table name*. If *Columns* is empty, all columns are retrieved. After outputting all relevant data, the operator becomes idle.

-   *Dynamic \(from input\)*: the operator uses each input message to determine the name of the source table and which columns to fetch. More details available in the [Input](read-hana-table-v2-b51aded.md#loiob51adedc86404c79afda7bbca3b958aa__section_d4d_5t3_cjb) section below.


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

The name of the source table in `Static` mode.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Columns

</td>
<td valign="top">

Columns

</td>
<td valign="top">

array

</td>
<td valign="top">

The list of columns that are retrieved in `Static` mode.

Default: \[\]

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

-   **Fraction**: decimals are represented as string in `"<numerator>/<denominator>"` format \(For example, `"3/4"`\).

-   **Floating-point**: decimals are converted to double-precision floating-point numbers represented as string.

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

Read Mode

</td>
<td valign="top">

readMode

</td>
<td valign="top">

array

</td>
<td valign="top">

Determines how the operator should read the table. Only used in `Static` mode.

Accepted values:

-   **Once**: The operator reads the table only once, then become idle.

-   **Poll**: The operator periodically polls the table for data.


Default: \[\]

</td>
</tr>
<tr>
<td valign="top">

Poll Period

</td>
<td valign="top">

pollPeriod

</td>
<td valign="top">

string

</td>
<td valign="top">

When *Read Mode* is set to *Poll*, this property determines the interval between consecutive queries.

Default: "1s"

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

Determines how the operator's output should be batched.

Accepted values:

-   **None**: no batching is performed. All rows in the target table are sent in a single output.

-   **Fixed size**: the output is broken into separate messages whose sizes is dictated by *Batch Size*. When placed in a group with multiplicity, the different instances of the operator take measures to avoid repetition.

    Refer to the [Multiplicity](read-hana-table-v2-b51aded.md#loiob51adedc86404c79afda7bbca3b958aa__section_xhv_nrj_cjb) section for details and examples.


Default: "None"

</td>
</tr>
<tr>
<td valign="top">

Batch Size

</td>
<td valign="top">

batchSize

</td>
<td valign="top">

integer

</td>
<td valign="top">

When *Batching* is set to *Fixed Size*, this property determines the number of rows in each output.

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

Default:"50s"

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



<a name="loiob51adedc86404c79afda7bbca3b958aa__section_d4d_5t3_cjb"/>

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

none

</td>
<td valign="top">

""

</td>
<td valign="top">

An input with an empty body containing the `com.sap.headers.hana.table` header with specific table details. This is only applicable in **Dynamic** mode.

</td>
</tr>
</table>



<a name="loiob51adedc86404c79afda7bbca3b958aa__section_krb_y1j_cjb"/>

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

A dynamic table described in the header `com.sap.headers.hana.table` together with the queried rows.

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

An error message as described at [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:. It depends on the **Error Handling**configuration.

</td>
</tr>
</table>



<a name="loiob51adedc86404c79afda7bbca3b958aa__section_x3p_x1b_pqb"/>

## State Management Support

State management support is provided when *Mode* is set to *Static* and *Batching* is set to *Fixed Size*, with *at-least-once* guarantee.

The state is saved between batches, so upon recovery, the operator doesn't have to start reading the table from the start. Instead, the read starts from the last batch index saved once the graph is resumed.



<a name="loiob51adedc86404c79afda7bbca3b958aa__section_xhv_nrj_cjb"/>

## Multiplicity

When configured to perform fixed-size batching, this operator takes its multiplicity into account when performing queries. Its instances progressively query the table in chunks of *Batch Size* rows, avoiding overlaps. Because each instance performs a separate query for each chunk, keep in mind that simultaneous changes to the source table may affect the behavior of this operator.

As an example, consider a source table of 65 rows and a `Read HANA Table` operator with multiplicity of 3 and *Batch Size* of 10. Assuming the table remains unchanged during execution, the following reads might take place \(due to concurrency, the order of events is not reliable\):

-   instance 0 outputs rows 0–9, 30–39, and 60–65;

-   instance 1 outputs rows 10–19 and 40–49;

-   instance 2 outputs rows 20–29 and 50–59.


