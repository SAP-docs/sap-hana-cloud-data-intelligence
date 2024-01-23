<!-- loio392e0b8e1d23415da1b66ed5baba1869 -->

# Similarity Score



Uses a convolutional neural network \(CNN\) model to calculate the similarity between two images. Currently, the InceptionV3 model, which is pretrained on the ImageNet dataset, is used. The output is a value in the range of 0.0 to 1.0. Values near 1.0 mean that images are very similar images, whereas values around 0.0 indicate images that are completely different. Possible input extensions are `jpg`, `jpe`, `jpeg`, `png`, `gif`, `bmp`, `tif`, and `tiff`.

> ### Note:  
> This operator is designed to work with two `readFile`-like operators, which should be connected to the `image` input port.



<a name="loio392e0b8e1d23415da1b66ed5baba1869__section_vy3_zfx_v4b"/>

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

image1

</td>
<td valign="top">

`message.file` 

</td>
<td valign="top">

Contains the binary content of an image of the given extensions.

</td>
</tr>
<tr>
<td valign="top">

image2

</td>
<td valign="top">

`message.file` 

</td>
<td valign="top">

Contains the binary content of an image of the given extensions.

</td>
</tr>
</table>



<a name="loio392e0b8e1d23415da1b66ed5baba1869__section_ozm_1gx_v4b"/>

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

similarity score

</td>
<td valign="top">

string

</td>
<td valign="top">

A stringified JSON containing the similarity score of the two given images.

</td>
</tr>
</table>

