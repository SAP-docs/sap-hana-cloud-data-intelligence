<!-- loioff0a160695ce486cb09011c8dcf62ca9 -->

# Py3 Type to Blob

This operator will serialize any Python3 data received in its input port and send the result to the output port. First, the data will try to be serialized by calling the method `to_blob()` on the data. If that doesn't work then the data will be serialized with protocol 2 of the pickle library.



<a name="loioff0a160695ce486cb09011c8dcf62ca9__section_hmx_wx4_j2b"/>

## Configuration Parameters

None



<a name="loioff0a160695ce486cb09011c8dcf62ca9__section_t41_4x4_j2b"/>

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

`input` 

</td>
<td valign="top">

python36.\*

</td>
<td valign="top">

Any Python3 data.

</td>
</tr>
</table>



<a name="loioff0a160695ce486cb09011c8dcf62ca9__section_wjj_px4_j2b"/>

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

`output` 

</td>
<td valign="top">

blob

</td>
<td valign="top">

The input serialized to bytes.

</td>
</tr>
</table>

