<!-- loiocf6b74cc9e974981b5bd7400a131ebec -->

# Table Messages

A table message is an SAP Data Intelligence Modeler message that represents tabular data. The port type for table messages is `message.table`.



## Attributes

All table messages have an attribute named “table” with a value that's an object. The object has the properties described in the following table.


<table>
<tr>
<th valign="top">

Property

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**version \(required\)**

</td>
<td valign="top">

Version of the table message type expressed as an integer.

</td>
</tr>
<tr>
<td valign="top">

**name**

</td>
<td valign="top">

Name of the table expressed as a string, such as the name of the database from which it came. If the name is case-insensitive, you must enter it in all uppercase letters. Otherwise, you must use the actual casing.

</td>
</tr>
<tr>
<td valign="top">

**columns**

</td>
<td valign="top">

Objects that describe each column of the table, expressed in an array. Each object has the following properties:

-   **Name**: String containing the name of the column. If the name is unknown, can be the empty string. If the name is case-insensitive, you must enter it in all uppercase letters. Otherwise, you must use the actual casing.

-   **Class**: String containing the type class of the column. If the type is unknown, must be an empty string or one of the [Supported types](table-messages-cf6b74c.md#loiocf6b74cc9e974981b5bd7400a131ebec__section_q5q_xdp_1xb). Class names are always lowercase.

-   **Type**: Object containing database-specific type information. The keys in this object must be the lower-case name of the database management system \(DBMS\), and each value a string with the type name.

-   **Size**: Integer that specifies the column size limit, where applicable.

-   **Precision and scale**: Integers specifying precision and scale of a decimal column.

-   **Nullable**: Boolean indicating whether the column accepts NULL values.




</td>
</tr>
<tr>
<td valign="top">

**primaryKey**

</td>
<td valign="top">

Name of the primary key column expressed as a string, or an array of column names for a compound key.

</td>
</tr>
</table>



<a name="loiocf6b74cc9e974981b5bd7400a131ebec__section_khf_nmy_cjb"/>

## Body

The message body must be an array of arrays of generic elements using Go language: `[][]interface{}`. The data in the body must always be row based. All rows must contain the same number of values.





### Supported Types

The term “class” refers to a group of similar column types commonly found in database management systems and file formats. For example, the string class can be found in the form of SQL types, such as VARCHAR and ALPHANUM.

The following table contains correspondence that is established between classes and the concrete data types used to hold their values.

> ### Note:  
> In the **Data type** column of the following table, “int” refers to these data types:
> 
> -   `int8`
> -   `uint8`
> -   `int16`
> -   `uint16`
> -   `int32`
> -   `uint32`
> -   `int64`
> -   `uint64`
> -   `int`
> -   `uint`


<table>
<tr>
<th valign="top">

Type Class

</th>
<th valign="top">

Data Type

</th>
<th valign="top">

String Format

</th>
</tr>
<tr>
<td valign="top">

timestamp

</td>
<td valign="top">

string

</td>
<td valign="top">

RFC 3339

RFC 3339 includes a numeric time zone \(or `Z` for UTC\) and an optional value of nanoseconds.

> ### Example:  
> `2006-01-02T15:04:05.999999999Z07:00`

Columns that store only part of a timestamp must leave the unused portion at the zero value \(midnight for the time and `0000-01-01` for the date\).

</td>
</tr>
<tr>
<td valign="top">

integer

</td>
<td valign="top">

int

</td>
<td valign="top">

integer

</td>
</tr>
<tr>
<td valign="top">

decimal

</td>
<td valign="top">

int / float64/ string

</td>
<td valign="top">

Decimal number with a dot as the separator or a fraction \(`numerator/denominator`\). You can suffix the int with the letter e followed by an exponent.

> ### Example:  
> <code>“1.43e-1”</code> for the value `0.143`.

Provide the value for a decimal by direct integer/float representation or as a string encapsulating a valid number.

> ### Example:  
> -   **Fraction:** `"numerator/denominator"` \(for example, `"3/4"`\).
> -   **Integer:** `"integer"` \(for example, `"50"`\).
> -   **Floating-point:** `"floating-point"` \(for example, `"2.5"`,`"1.43e-1"`\).



</td>
</tr>
<tr>
<td valign="top">

float

</td>
<td valign="top">

float64

</td>
<td valign="top">

Decimal number with a dot as the separator or a fraction \(`numerator/denominator`\). You can suffix the int with the letter e followed by an exponent.

> ### Example:  
> <code>“1.43e-1”</code> for the value `0.143`.



</td>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

binary

</td>
<td valign="top">

\[\]byte

</td>
<td valign="top">

Base 64 \(RFC 4648, padded\)

</td>
</tr>
<tr>
<td valign="top">

bool

</td>
<td valign="top">

bool

</td>
<td valign="top">

`1`, `t`, `T`, `TRUE`, `true`, `True`, `0`, `f`, `F`, `FALSE`, `false`, or `False`

</td>
</tr>
</table>

When a column's class is unknown, the engine can leave the operators' values as strings. Later in the graph, if a particular class is expected for that column, it's possible to choose to convert its values. In this case, the operator engine understands that the string is in the format specified under the **String format** column in the table. For example, when the operator is reading from a CSV file to insert its data into an existing database table: Column classes are unknown when parsing CSV, but some database operators require the table schema from the server and treat each column accordingly.



<a name="loiocf6b74cc9e974981b5bd7400a131ebec__section_x4z_hpy_cjb"/>

## Encoding

Even if an operator input is a general type of `message.*` or `any.*`, you must set the encoding to table so that operators can detect a table message.



<a name="loiocf6b74cc9e974981b5bd7400a131ebec__section_a4y_kpy_cjb"/>

## Examples



### Parsing CSV

> ### Example:  
> The following CSV data has a header for the first line \(the column names\):
> 
> ```
> ID,NAME,BIRTH,INTERNAL
> 0,John Doe,15-04-1982,no
> 1,Nancy Milburn,24-11-1991,yes
> ```
> 
> The CSV parser outputs the following table message \(represented in JSON\):
> 
> ```
> {
>     "Attributes": {
>         "table": {
>             "version": 1,
>             "columns": [
>                 {"name": "ID"},
>                 {"name": "NAME"},
>                 {"name": "BIRTH"},
>                 {"name": "INTERNAL"},
>             ]
>         }
>     },
>     "Encoding": "table",
>     "Body": [
>         ["0", "John Doe", "15-04-1982", "no"],
>         ["1", "Nancy Milburn", "24-11-1991", "yes"]
>     ]
> }
> ```
> 
> Because the formats for timestamp and Boolean don't comply with the formats expected for a table message, you can use an intermediate operator to adapt the format into the following:
> 
> ```
> {
>     "Attributes": {
>         "table":{
>             "version": 1,
>             "columns": [
>                 {"name": "ID"},
>                 {"name": "NAME"},
>                 {"name": "BIRTH", "class": "timestamp"},
>                 {"name": "INTERNAL", "class": "bool"}
>             ]
>         }
>     },
>     "Encoding": "table",
>     "Body": [
>         ["0", "John Doe", "1982-04-15T00:00:00Z", false],
>         ["1", "Nancy Milburn", "1991-11-24T00:00:00Z", true]
>     ]
> }
> ```



### Querying Database

> ### Example:  
> The following table exists on an SAP HANA database:
> 
> 
> <table>
> <tr>
> <th valign="top">
> 
> ID \(`BIGINT`\)
> 
> </th>
> <th valign="top">
> 
> SALARY \(`DECIMAL(10,2)`\)
> 
> </th>
> <th valign="top">
> 
> HIRED \(`DATE`\)
> 
> </th>
> </tr>
> <tr>
> <td valign="top">
> 
> 0
> 
> </td>
> <td valign="top">
> 
> 4560.50
> 
> </td>
> <td valign="top">
> 
> '2003-01-14'
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> 1
> 
> </td>
> <td valign="top">
> 
> 8740.50
> 
> </td>
> <td valign="top">
> 
> '2001-07-28'
> 
> </td>
> </tr>
> </table>
> 
> If an operator runs a `SELECT` statement on this table and outputs the values in a table message, the following format is expected:
> 
> ```
> {
>     "Attributes": {
>         "table": {
>             "version": 1,
>             "columns": [
>                 {"name": "ID", "class": "integer", "type": {"hana": "BIGINT"}},
>                 {"name": "SALARY", "class": "decimal", "precision": 10, "scale": 2, "type": {"hana": "DECIMAL"}},
>                 {"name": "HIRED", "class": "timestamp", "type": {"hana": "DATE"}},
>             ],
>             "primaryKey": "ID"
>         }
>     },
>     "Encoding": "table",
>     "Body": [
>         [0, 4560.50, "2003-01-14T00:00:00Z"],
>         [1, 8740.50, "2001-07-28T00:00:00Z"]
>     ]
> }
> ```
> 
> When there's a fraction \(string\) as decimal output format, such as in the `456 0.50` and `8740.50` in the sample code, the values are represented as `"9121/2"` and `"17481/2"`, respectively.

