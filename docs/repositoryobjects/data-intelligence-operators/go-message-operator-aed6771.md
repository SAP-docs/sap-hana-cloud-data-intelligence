<!-- loioaed6771c7cb644d69aca286ceb01a575 -->

# Go Message Operator

This Go operator is an example of how to use message type with a Go script.



<a name="loioaed6771c7cb644d69aca286ceb01a575__section_zj5_lc1_j2b"/>

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

codelanguage

</td>
<td valign="top">

string

</td>
<td valign="top">

The programming language used in the code.

Default: "go"

</td>
</tr>
<tr>
<td valign="top">

script

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The inline script to be executed. If the script starts with `file://`, then the script file is executed.

Default: ""

</td>
</tr>
</table>



<a name="loioaed6771c7cb644d69aca286ceb01a575__section_hkj_qc1_j2b"/>

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

`input` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Any message which body should be converted to an uppercase string.

</td>
</tr>
</table>



<a name="loioaed6771c7cb644d69aca286ceb01a575__section_scp_5c1_j2b"/>

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

message

</td>
<td valign="top">

The message which body contains an uppercase string.

</td>
</tr>
</table>

For further information about customizing the `Go` operator, refer to the base [Go Operator](go-operator-aabb1ca.md) documentation.

