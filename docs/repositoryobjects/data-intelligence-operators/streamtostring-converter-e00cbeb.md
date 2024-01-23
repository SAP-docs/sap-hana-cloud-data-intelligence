<!-- loioe00cbeba2f0b403e9174aea4d0958157 -->

# StreamToString Converter

This operator parses a contiguous stream of strings and breaks them at platform-dependent line delimiters into separate output strings.



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

Unescape

</td>
<td valign="top">

unescape

</td>
<td valign="top">

bool

</td>
<td valign="top">

If set to "True", the previously escaped "\\" and "\\n" have the escaping character removed \(see [StringToStream Converter](stringtostream-converter-a59d48f.md)\)

Default: false

</td>
</tr>
</table>



<a name="loioe00cbeba2f0b403e9174aea4d0958157__section_j3t_ykc_xdb"/>

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

stream.\*

</td>
<td valign="top">

The input stream to be parsed.

</td>
</tr>
</table>



<a name="loioe00cbeba2f0b403e9174aea4d0958157__section_t4t_jlc_xdb"/>

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

string.\*

</td>
<td valign="top">

The strings parsed from the incoming stream.

</td>
</tr>
</table>

