<!-- loio1508faf4dfed43e8994ce1db8856bf68 -->

# ToNumber Converter

The ToNumber Converter operator converts types int64, uint64, float64, and string into other numeric types. When converting from float64, you can also choose the rounding behavior. If converting from a string, the content of the string must be numerical.



> ### Note:  
> The current version of this operator does not handle representation overflow when converting, for example, from uint64 to int64 and will raise an error upon encountering this scenario.



<a name="loio1508faf4dfed43e8994ce1db8856bf68__section_zj5_lc1_j2b"/>

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

Rounding Behavior

</td>
<td valign="top">

roundingBehavior

</td>
<td valign="top">

string

</td>
<td valign="top">

How rounding will behave when converting from a float64 type.

Default: "up"

</td>
</tr>
</table>



<a name="loio1508faf4dfed43e8994ce1db8856bf68__section_hkj_qc1_j2b"/>

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

any\*

</td>
<td valign="top">

The input value, which can be of types int64, uint64, float64, and string.

</td>
</tr>
</table>



<a name="loio1508faf4dfed43e8994ce1db8856bf68__section_scp_5c1_j2b"/>

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

`outFloat` 

</td>
<td valign="top">

float64

</td>
<td valign="top">

The input value converted to type float64.

</td>
</tr>
<tr>
<td valign="top">

`outInt` 

</td>
<td valign="top">

int64

</td>
<td valign="top">

The input value converted to type int64.

</td>
</tr>
<tr>
<td valign="top">

`outUint` 

</td>
<td valign="top">

uint64

</td>
<td valign="top">

The input value converted to type uint64.

</td>
</tr>
</table>

