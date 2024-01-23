<!-- loioeee668eb003f49a48ccad76c06d4b7ad -->

# ToMessage Converter

The ToMessage Converter operator converts the input to a Modeler message. The input can be either a string representation of the entire message or a data of any type that will be placed in the body of a new message.



## Configuration Parameters

None



<a name="loioeee668eb003f49a48ccad76c06d4b7ad__section_u35_33c_xdb"/>

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

`inbody` 

</td>
<td valign="top">

any.\*

</td>
<td valign="top">

When any data arrives in this port, a new message is created with the received data placed in its body. The attributes and encoding fields are left empty.

</td>
</tr>
<tr>
<td valign="top">

`instring` 

</td>
<td valign="top">

string

</td>
<td valign="top">

The input string that represents the entire messsage. For example, the string: `{"message.attributes.encoding`": "`jpeg`", "`otherField`":`3}this part is the body`' will be converted to a message where the body has the string "`this part is the body`", the attributes has the map `{"otherField": 3}`, and the bodyEncoding has the string "`jpeg`". The body will always become a string when this port is used.

</td>
</tr>
</table>



<a name="loioeee668eb003f49a48ccad76c06d4b7ad__section_jxw_y3c_xdb"/>

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

The resulting Modeler message derived from the input.

</td>
</tr>
</table>

