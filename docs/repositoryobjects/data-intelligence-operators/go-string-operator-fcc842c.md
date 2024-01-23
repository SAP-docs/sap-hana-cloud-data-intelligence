<!-- loiofcc842c7586c4434be5789c8511ac5b9 -->

# Go String Operator

This Go operator increments and outputs a counter value with the input, based on a Go script.



<a name="loiofcc842c7586c4434be5789c8511ac5b9__section_zj5_lc1_j2b"/>

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



<a name="loiofcc842c7586c4434be5789c8511ac5b9__section_hkj_qc1_j2b"/>

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

string

</td>
<td valign="top">

Any string that should be output with the counter.

</td>
</tr>
</table>



<a name="loiofcc842c7586c4434be5789c8511ac5b9__section_scp_5c1_j2b"/>

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

string

</td>
<td valign="top">

The string appended to counter value.

</td>
</tr>
</table>

For further information about customizing the Go String operator, refer to the base [Go Operator](go-operator-aabb1ca.md) documentation.

