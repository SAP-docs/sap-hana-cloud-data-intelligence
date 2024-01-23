<!-- loioa59d48f7c5f5453694462a0b20c9f29f -->

# StringToStream Converter

This operator converts incoming strings into a contiguous stream. A platform-dependent line delimiter is appended after each string written to the output stream.



## Configuration Parameters

****


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

Escape

</td>
<td valign="top">

escape

</td>
<td valign="top">

bool

</td>
<td valign="top">

If set to True, the sequences \\ \(backslash\) and \\n \(new line\) are escaped.

\(See [StringToStream Converter](stringtostream-converter-a59d48f.md).\)

Default: false

</td>
</tr>
</table>



<a name="loioa59d48f7c5f5453694462a0b20c9f29f__section_j3t_ykc_xdb"/>

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

`in` 

</td>
<td valign="top">

string.\*

</td>
<td valign="top">

The string inputs.

</td>
</tr>
</table>



<a name="loioa59d48f7c5f5453694462a0b20c9f29f__section_t4t_jlc_xdb"/>

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

`out` 

</td>
<td valign="top">

stream.\*

</td>
<td valign="top">

The contiguous stream of input parameters delimited by a platform-dependent line delimiter.

</td>
</tr>
</table>

