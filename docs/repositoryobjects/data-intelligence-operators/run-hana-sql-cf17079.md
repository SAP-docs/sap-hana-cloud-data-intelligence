<!-- loiocf17079de4504558b0ea1c2a54b45151 -->

# Run HANA SQL

The Run HANA SQL operator executes user-provided SQL statements on an SAP HANA database.



<a name="loiocf17079de4504558b0ea1c2a54b45151__section_b3g_vnj_cjb"/>

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

Determines how the operator obtains the SQL code.

Accepted values:

-   *Static \(from configuration\)*: the operator executes the statement\(s\) specified in **SQL** and becomes idle.

-   *Dynamic \(from input\)*: the operator executes SQL statement\(s\) from each input message.


Default: " "

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

Determines how the operator outputs the values for columns of type `DECIMAL` and `SMALLDECIMAL`.

Accepted values:

-   `Fraction (string)`: decimals are represented as string in `"<numerator>/<denominator>"` format \(for example, `"3/4"`\).

-   `Floating-point`: decimals are converted to double-precision floating-point numbers.

    > ### Note:  
    > The resulting number may not represent the exact value of the division as there can be a loss of precision.


Default: "Fraction \(string\)"

</td>
</tr>
<tr>
<td valign="top">

CESU-8 Output Handling

</td>
<td valign="top">

cesu8OutputHandling

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines how the operator deals with CESU-8 encoding problems. Such situation can happen due to the conversion from UTF-16 \(used in ABAP systems\) to CESU-8/UTF-8 used internally to represent the values as strings. This only affects character- based field types.

Accepted values:

-   `Default`: the operator throws an error describing the column and row that caused the problem.

    > ### Example:  
    > ```
    >   invalid CESU-8: <FIELD_VALUE> at pos: <POSITION> row: 0 fieldname: <COLUMN_NAME>
    > 
    > ```

-   `Replace`: incorrectly encoded CESU-8 chars are replaced with the Unicode replacement char \(`'\uFFFD'`\).
-   `Raw`: the data is represented by the exact bytes stored in the database field with no transformation.

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


In **Dynamic** mode, each input message may override this configuration by setting the `transactionLevel` property in the `hana` object:

```
  msg.Attributes.hana = { transactionLevel: "Per input" };

```

This applies exclusively to that input and bears no effect over upcoming ones.

Default: "Per input"

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



<a name="loiocf17079de4504558b0ea1c2a54b45151__section_d4d_5t3_cjb"/>

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

message.\*

</td>
<td valign="top">

A message whose body is a string containing SQL commands. This only applies to **Dynamic** mode.

</td>
</tr>
</table>



<a name="loiocf17079de4504558b0ea1c2a54b45151__section_krb_y1j_cjb"/>

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

A Table Message \([Table Messages](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/cf6b74cc9e974981b5bd7400a131ebec.html "A table message is an SAP Data Intelligence Modeler message that represents tabular data. The port type for table messages is message.table.") :arrow_upper_right:\) holding retrieved data. For statements that do not query data, an empty table is output to signal completion.

In **Dynamic** mode, this output also includes any additional attributes that were present in the input.

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

