<!-- loio6dd943c725e84878b9c422f961744ebb -->

# ToBlob Converter

The ToBlob Converter operator converts the input into a byte array. When data is received at inInterface, the following conversion is performed:



-   primitive number types: a big-endian byte array representation.

-   string: a standard conversion.




<a name="loio6dd943c725e84878b9c422f961744ebb__section_v3k_thc_xdb"/>

## Configuration Parameters

None



<a name="loio6dd943c725e84878b9c422f961744ebb__section_zpt_5hc_xdb"/>

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

`inInterface` 

</td>
<td valign="top">

any

</td>
<td valign="top">

The input interface.

</td>
</tr>
</table>



<a name="loio6dd943c725e84878b9c422f961744ebb__section_gb4_zhc_xdb"/>

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

`outByteArray` 

</td>
<td valign="top">

blob

</td>
<td valign="top">

The output byte array.

</td>
</tr>
</table>

