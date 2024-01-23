<!-- loiodf20169a16734218be7f09754b88f4fc -->

# Topic Detection



Uses Non-negative Matrix Factorization \(NMF\) to predict topics from the text document samples. The language of the input text document must be English.

Accepted file input extensions are `zip`, `tar`, `tar.gz`, and `txt`.

> ### Note:  
> This operator is designed to work together with a `Read File`-like operator, which should be connected to the `file` input port.



<a name="loiodf20169a16734218be7f09754b88f4fc__section_cfq_z24_dpb"/>

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

Topic Number

</td>
<td valign="top">



</td>
<td valign="top">

number

</td>
<td valign="top">

Mandatory. The number of topics to be extracted from the text documents. The Topic Number should be less than or equal to the min\(number of text documents, Keywords Number per Topic\).

Default: none

</td>
</tr>
<tr>
<td valign="top">

Keywords Number per Topic

</td>
<td valign="top">



</td>
<td valign="top">

number

</td>
<td valign="top">

Mandatory. The number of keywords to be extracted for each topic.

Default: none

</td>
</tr>
<tr>
<td valign="top">

Max Feature Number

</td>
<td valign="top">



</td>
<td valign="top">

number

</td>
<td valign="top">

Optional. The maximum feature number to be extracted in the corpus vectorization process.

Default: 20

</td>
</tr>
</table>



<a name="loiodf20169a16734218be7f09754b88f4fc__section_vy3_zfx_v4b"/>

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

file

</td>
<td valign="top">

`message.file` 

</td>
<td valign="top">

Contains the binary content of a text file or an archive file of the given extensions.

</td>
</tr>
</table>



<a name="loiodf20169a16734218be7f09754b88f4fc__section_ozm_1gx_v4b"/>

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

A stringified JSON containing the predicted topics of given documents

</td>
</tr>
</table>

