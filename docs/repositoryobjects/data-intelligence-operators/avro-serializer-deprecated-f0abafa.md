<!-- loiof0abafa2af20437aa13333e3ac5ea9bc -->

# Avro Serializer \(Deprecated\)

The Avro Serializer operator converts CSV encoded lines and produces the contents as Avro encoded messages. It does not support nested records.



> ### Note:  
> This operator is deprecated. Use the operators [Avro Decoder](avro-decoder-1509d8f.md) and [Avro Encoder](avro-encoder-1676e87.md) instead. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loiof0abafa2af20437aa13333e3ac5ea9bc__section_sq1_nf3_vdb"/>

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

Avro Schema

</td>
<td valign="top">

avroSchema



</td>
<td valign="top">

string

</td>
<td valign="top">

Avro schema used to read fields names and types.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Delimiter

</td>
<td valign="top">

delimiter

</td>
<td valign="top">

rune

</td>
<td valign="top">

Ascii code for delimiter character, the default is "," code.

Default: 44

</td>
</tr>
<tr>
<td valign="top">

Header Included

</td>
<td valign="top">

headerIncluded

</td>
<td valign="top">

bool

</td>
<td valign="top">

Used to indicate if there is a header on CSV first line.

Default: true

</td>
</tr>
<tr>
<td valign="top">

Include Schema

</td>
<td valign="top">

includeSchema

</td>
<td valign="top">

bool

</td>
<td valign="top">

The schema should be included on avro message.

Default: false

</td>
</tr>
</table>



<a name="loiof0abafa2af20437aa13333e3ac5ea9bc__section_knq_5f3_vdb"/>

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

message

</td>
<td valign="top">

Message with CSV in the body.

</td>
</tr>
</table>



<a name="loiof0abafa2af20437aa13333e3ac5ea9bc__section_swc_cg3_vdb"/>

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

message

</td>
<td valign="top">

Avro representation of the input message.

</td>
</tr>
</table>

