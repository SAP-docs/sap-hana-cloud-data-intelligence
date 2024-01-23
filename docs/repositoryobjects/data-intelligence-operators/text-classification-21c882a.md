<!-- loio21c882a6964f4e00a634b291e519c4f3 -->

# Text Classification



Uses a Random Forest Classifier model to predict the class of a given text input. The operator is designed to classify one input at each step and receives a string as input.

> ### Note:  
> This operator is designed to work together with a `dataGenerator`-like operator, which should be connected to the text input port.



<a name="loio21c882a6964f4e00a634b291e519c4f3__section_vy3_zfx_v4b"/>

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

text

</td>
<td valign="top">

`string` 

</td>
<td valign="top">

Contains a text string to be used as input.

</td>
</tr>
</table>



<a name="loio21c882a6964f4e00a634b291e519c4f3__section_ozm_1gx_v4b"/>

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

prediction

</td>
<td valign="top">

string

</td>
<td valign="top">

A stringified JSON containing, by default, the five highest scoring classes of the given text. \(This amount can be changed by the user.\)

</td>
</tr>
</table>

