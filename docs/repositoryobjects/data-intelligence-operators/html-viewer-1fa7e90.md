<!-- loio1fa7e90f5d3341a1bb36b97b3185d2a0 -->

# HTML Viewer

The HTML Viewer operator renders HTML code on the browser as it arrives at the input port.



This operator renders HTML code on the browser as it arrives at the input port.

`script` tags are ignored by the operator, but CSS in `style` tags are accepted.



<a name="loio1fa7e90f5d3341a1bb36b97b3185d2a0__section_mqb_jjk_tgb"/>

## Configuration Parameters

None



<a name="loio1fa7e90f5d3341a1bb36b97b3185d2a0__section_r4z_kjk_tgb"/>

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

`in1`

</td>
<td valign="top">

string.\*

</td>
<td valign="top">

A string containing HTML code to be rendered.

</td>
</tr>
</table>



<a name="loio1fa7e90f5d3341a1bb36b97b3185d2a0__section_hwr_vjk_tgb"/>

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

`out1`

</td>
<td valign="top">

string.\*

</td>
<td valign="top">

Relays the same string that is received.

</td>
</tr>
</table>

