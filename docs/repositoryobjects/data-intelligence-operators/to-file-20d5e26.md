<!-- loio20d5e267ade3459f920df194b49aaa70 -->

# To File

This operator converts the input to a file message, taking either the payload or path. Note that the input ports are independent, and each input generates one output.



If the input comes from the port path, it is used as the path property in the resulting file message, leaving the payload empty.

If the input comes from the port in, it is used as the payload \(body\) of the resulting message. If in is connected to a message, it keeps the incoming file attribute or populates with an empty one if none is given, maintaining the body as the payload of the file. Payload incoming types are mapped as follows:

****


<table>
<tr>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">

Used as-is

</td>
</tr>
<tr>
<td valign="top">

blob

</td>
<td valign="top">

Used as-is

</td>
</tr>
<tr>
<td valign="top">

other

</td>
<td valign="top">

Converted to JSON

</td>
</tr>
</table>



<a name="loio20d5e267ade3459f920df194b49aaa70__section_qdh_d3k_cjb"/>

## Configuration Parameters

-   None.




<a name="loio20d5e267ade3459f920df194b49aaa70__section_knq_5f3_vdb"/>

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

in

</td>
<td valign="top">

any.\*

</td>
<td valign="top">

The payload of the file. It generates a file message using the input as the payload. If the input is a message, incoming attributes are kept, including the file properties; otherwise, they are populated with an empty path and connection.

</td>
</tr>
<tr>
<td valign="top">

path

</td>
<td valign="top">

any.\*

</td>
<td valign="top">

The path of the file. It generates a file message as output with an empty body and the received path. If the input is a message, the body is used as the path and incoming attributes are kept, including any other file property besides the path.

</td>
</tr>
</table>



<a name="loio20d5e267ade3459f920df194b49aaa70__section_swc_cg3_vdb"/>

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

file

</td>
<td valign="top">

message.file

</td>
<td valign="top">

A file with the given payload or path.

</td>
</tr>
</table>

