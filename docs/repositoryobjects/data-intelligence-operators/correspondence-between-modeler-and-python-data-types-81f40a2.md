<!-- loio81f40a2d186b480596dfc2cfa365df4c -->

# Correspondence Between Modeler and Python Data Types

The SAP Data Intelligence Modeler data types are types that are allowed in the operator ports. The Modeler translates Phthon3 data types to supported data types.

> ### Example:  
> If you have an input port of type `blob`, then the Python object that you receive as an argument to your port callback is of type `bytes`. If the output port of your operator has the type `string`, then you send a Python object of type `str` in its output port.

The following table shows the Modeler data types and the corresponding Python3 data types.


<table>
<tr>
<th valign="top">

Modeler

</th>
<th valign="top">

Python3

</th>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">

str

</td>
</tr>
<tr>
<td valign="top">

blob

</td>
<td valign="top">

bytes

</td>
</tr>
<tr>
<td valign="top">

int64

</td>
<td valign="top">

int

</td>
</tr>
<tr>
<td valign="top">

uint64

</td>
<td valign="top">

int

</td>
</tr>
<tr>
<td valign="top">

float664

</td>
<td valign="top">

float

</td>
</tr>
<tr>
<td valign="top">

byte

</td>
<td valign="top">

int

</td>
</tr>
<tr>
<td valign="top">

message

</td>
<td valign="top">

Message

</td>
</tr>
</table>

