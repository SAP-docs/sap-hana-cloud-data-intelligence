<!-- loiod9222a68cb034725ba040903624bd0a6 -->

# Histogram Plotter

The Histogram Plotter operator receives a string-converted Data Pipeline message as input with an array of integers in the body and rangeMin and rangeMax fields in the header.



It then generates a vertical bar plot with one bar corresponding to each position in the received array. The rangeMin and rangeMax fields are used to make the tick marks in the x axis. There are two y axis. The left y axis represents values of the array as percentages \(position i: 100\*array\[i\]/sum\(array\)\). The right y axis shows the actual value in the array. Both y axis have 10 tick marks.



<a name="loiod9222a68cb034725ba040903624bd0a6__section_n2f_kxc_12b"/>

## Configuration Parameters

None



<a name="loiod9222a68cb034725ba040903624bd0a6__section_p2f_kxc_12b"/>

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

`in1` 

</td>
<td valign="top">

string

</td>
<td valign="top">

A string-converted Data Pipeline message with an array of integers in the body. The array should be formatted as a JSON array. The header should contain the fields rangeMin and rangeMax. Use the toStringConverter operator to convert the output of the Histogram operator to give the correct format for this operator input.

</td>
</tr>
</table>



<a name="loiod9222a68cb034725ba040903624bd0a6__section_r2f_kxc_12b"/>

## Output

None

