<!-- loio76055ab8319a4bbda5b65906535a4955 -->

# Generate Table

This operator can generate Table Messages with a user-defined schema and random data.



<a name="loio76055ab8319a4bbda5b65906535a4955__section_sq1_nf3_vdb"/>

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

Configuration Mode

</td>
<td valign="top">

configMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Specifies how the operator will obtain metadata to generate tables.

Accepted values:

-   Static \(from configuration\): the name, columns and primary key\(s\) of the generated table\(s\) will be determined by the respective configuration values.

-   Dynamic \(from input\): the name, columns and primary key\(s\) of the generated table\(s\) will be determined by the input Table Message.


Default: ""

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

The name of the generated table in Static mode.

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

The column definition for the table\(s\) generated in Static mode.

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

A list of strings holding the name\(s\) of the column\(s\) that compose the table's primary key.

Default: \[\]

</td>
</tr>
<tr>
<td valign="top">

Output Mode

</td>
<td valign="top">

outputMode

</td>
<td valign="top">

string

</td>
<td valign="top">

In Static mode, it determines when the operator should generate tables.

Accepted values:

-   Once: the operator will output a single table, then become idle.

-   Periodic: the operator periodically outputs a table.

-   Trigger: the operator outputs a table upon receiving the set number of inputs \(see Trigger count\).


Default: "Once"

</td>
</tr>
<tr>
<td valign="top">

Period

</td>
<td valign="top">

period

</td>
<td valign="top">

string

</td>
<td valign="top">

When in Periodic mode, this property determines the interval between consecutive outputs.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Trigger Count

</td>
<td valign="top">

triggerCount

</td>
<td valign="top">

integer

</td>
<td valign="top">

When in Trigger mode, this property sets the number of inputs that should be received before triggering each output.

Default: 1

</td>
</tr>
<tr>
<td valign="top">

Rows per Output

</td>
<td valign="top">

rowsPerOutput

</td>
<td valign="top">

integer

</td>
<td valign="top">

The number of rows of random data to be generated for each output table. May be set to zero for empty tables.

Default: 5

</td>
</tr>
</table>



<a name="loio76055ab8319a4bbda5b65906535a4955__section_knq_5f3_vdb"/>

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

`trigger` 

</td>
<td valign="top">

any.\*

</td>
<td valign="top">

In Static mode, this input is consumed only if Output mode is set to Trigger. In this case, the value itself is ignored and may be of any type.

In Dynamic mode, the input must be a Table Message describing the table to be generated.

</td>
</tr>
</table>



<a name="loio76055ab8319a4bbda5b65906535a4955__section_swc_cg3_vdb"/>

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

`output` 

</td>
<td valign="top">

message.table

</td>
<td valign="top">

A Table Message generated according to the requested schema. If Rows per output is greater than zero, the message body will have randomly-generated data of the appropriate type for each column.

</td>
</tr>
</table>

