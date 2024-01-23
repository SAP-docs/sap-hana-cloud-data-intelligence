<!-- loio1676e878b58c4f97ad4439537eae7c95 -->

# Avro Encoder

The Avro Encoder operator allows you to create Avro, CSV, or JSON messages from messages containing record objects.



This operator can be used as the inverse operator of the [Avro Decoder](avro-decoder-1509d8f.md) operator to reconstruct the original messages or the equivalent messages in another format or different structures.

The schema must be provided as an Avro schema in this operator's configuration or included in the message itself under attribute "avro.schema". This schema is used to assemble the input data into the target output message.

For the mapping of values across different representation domains, refer to the mapping table in [Avro Decoder](avro-decoder-1509d8f.md).



<a name="loio1676e878b58c4f97ad4439537eae7c95__section_sq1_nf3_vdb"/>

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

defaultAvroSchema

</td>
<td valign="top">

string

</td>
<td valign="top">

The Avro schema to be used to generate the output message.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

format

</td>
<td valign="top">

string

</td>
<td valign="top">

The output message format. The accepted values are "avro", "csv", or "json".

Default: "avro"

</td>
</tr>
<tr>
<td valign="top">

csvComma

</td>
<td valign="top">

rune

</td>
<td valign="top">

The delimiter character code for the CSV format. For example, 44 for ','; 59 for ';'; 124 for '|'.

Default: ","

</td>
</tr>
<tr>
<td valign="top">

csvHeaderIncluded

</td>
<td valign="top">

bool

</td>
<td valign="top">

The input CSV message contains the header line.

Default: false

</td>
</tr>
</table>



<a name="loio1676e878b58c4f97ad4439537eae7c95__section_knq_5f3_vdb"/>

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

Accept messages containing record objects in the body.

</td>
</tr>
</table>



<a name="loio1676e878b58c4f97ad4439537eae7c95__section_swc_cg3_vdb"/>

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

Messages whose body content are formatted as Avro, CSV, or JSON messages.

</td>
</tr>
<tr>
<td valign="top">

`error` 

</td>
<td valign="top">

message

</td>
<td valign="top">

If this port is not connected, any processing error will lead to the termination of the operator. If this port is connected, a message containing the original header attributes \(that is, all except `message.commit.token` and an additional attribute `message.response.error` set to the error\) and the body payload is emitted from this port.

</td>
</tr>
</table>

