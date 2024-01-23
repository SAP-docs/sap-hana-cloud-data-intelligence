<!-- loio402e6b628a274d80adc1c3a30bb9dde0 -->

# Node.js Data Types

SAP Data Intelligence maps Modeler data types to the Node.js JavaScript data types.

Inside a Node.js operator, you use JavaScript types and data structures. The following table shows the SAP Data Intelligence Modeler data types and the corresponding JavaScript data types:


<table>
<tr>
<th valign="top">

Modeler Data Type

</th>
<th valign="top">

JavaScript Data Type

</th>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">

String

</td>
</tr>
<tr>
<td valign="top">

blob

</td>
<td valign="top">

Buffer

</td>
</tr>
<tr>
<td valign="top">

int64

</td>
<td valign="top">

Number

</td>
</tr>
<tr>
<td valign="top">

uint64

</td>
<td valign="top">

Number

</td>
</tr>
<tr>
<td valign="top">

float64

</td>
<td valign="top">

Number

</td>
</tr>
<tr>
<td valign="top">

byte

</td>
<td valign="top">

Number

</td>
</tr>
<tr>
<td valign="top">

message

</td>
<td valign="top">

Object

</td>
</tr>
<tr>
<td valign="top">

\[ \]x

</td>
<td valign="top">

Array

</td>
</tr>
</table>

Replace the letter x in \[ \]x \(the last row of the table\) with any of the allowed data types \(except for message\). For example, \[ \]string, \[ \]uint64, \[ \]\[ \]blob, and so on. The Node.js subengine always does the conversion. If data reaches the Node.js operator script, it's converted already based on the conversions shown in the table.

> ### Note:  
> Always use the SAP Data Intelligence Modeler data types to specify the data types of the in and out ports in the `operator.json` file. This mapping is necessary, for example, if you develop a vsolution using an external project.

