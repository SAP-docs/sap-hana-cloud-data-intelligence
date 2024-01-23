<!-- loio1760e5289ae1477493eeb5f2e0c18c88 -->

# Flowgraph Compiler \(Deprecated\)

Does a flowgraph conversion.



> ### Note:  
> This operator is deprecated.



<a name="loio1760e5289ae1477493eeb5f2e0c18c88__section_sq1_nf3_vdb"/>

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

Flowgraph Type

</td>
<td valign="top">

Flowgraph type

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Flowgraph Type.

Default: "basic"

</td>
</tr>
<tr>
<td valign="top">

Reference Directory Location

</td>
<td valign="top">

Reference directory location

</td>
<td valign="top">

string

</td>
<td valign="top">

Reference directory location.

Default: "/tmp"

</td>
</tr>
<tr>
<td valign="top">

Side Effect Location

</td>
<td valign="top">

Side effect location

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Side effect location.

Default: "/tmp"

</td>
</tr>
</table>



<a name="loio1760e5289ae1477493eeb5f2e0c18c88__section_knq_5f3_vdb"/>

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

string

</td>
<td valign="top">

The flowgraph description.

</td>
</tr>
</table>



<a name="loio1760e5289ae1477493eeb5f2e0c18c88__section_swc_cg3_vdb"/>

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

blob

</td>
<td valign="top">

The `jar` file.

</td>
</tr>
<tr>
<td valign="top">

`outmessage` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The body of the message containing the `jar` file and its attributes containing the Spark configuration file.

</td>
</tr>
</table>

