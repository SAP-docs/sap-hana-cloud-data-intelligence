<!-- loioc265c32164c14f6ca0bcd820f3b9e333 -->

# Avro Deserializer \(Deprecated\)

The Avro Deserializer operator converts Avro-encoded messages and produces the contents as CSV-encoded lines.



> ### Note:  
> This operator is deprecated. Use the operators [Avro Decoder](avro-decoder-1509d8f.md) and [Avro Encoder](avro-encoder-1676e87.md) instead. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loioc265c32164c14f6ca0bcd820f3b9e333__section_sq1_nf3_vdb"/>

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

codeSchema

</td>
<td valign="top">

codecSchema

</td>
<td valign="top">

string

</td>
<td valign="top">

The Avro schema used for input message encoding.

Default: ""

</td>
</tr>
</table>



<a name="loioc265c32164c14f6ca0bcd820f3b9e333__section_knq_5f3_vdb"/>

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

The Avro-encoded message.

</td>
</tr>
</table>



<a name="loioc265c32164c14f6ca0bcd820f3b9e333__section_swc_cg3_vdb"/>

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

A CSV representation of the input message.

</td>
</tr>
</table>

