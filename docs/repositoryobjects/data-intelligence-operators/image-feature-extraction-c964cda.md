<!-- loioc964cdaa486b413cba25a09045b3bc68 -->

# Image Feature Extraction



Uses a convolutional neural network \(CNN\) model to predict a flattened 131072 feature vector \(unflattened 2048 feature vectors of shape \(8,8\)\). Currently, the InceptionV3 model, which is pretrained on the ImageNet dataset, is used. The operator is designed to extract one vector at each step. Possible input extensions are `jpg`, `jpe`, `jpeg`, `png`, `gif`, `bmp`, `tif`, and `tiff`.

> ### Note:  
> This operator is designed to work with a `readFile`-like operator, which should be connected to the `image` input port.



<a name="loioc964cdaa486b413cba25a09045b3bc68__section_vy3_zfx_v4b"/>

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

image

</td>
<td valign="top">

`message.file` 

</td>
<td valign="top">

Contains the binary content of an image of the given extensions.

</td>
</tr>
</table>



<a name="loioc964cdaa486b413cba25a09045b3bc68__section_ozm_1gx_v4b"/>

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

features

</td>
<td valign="top">

string

</td>
<td valign="top">

A stringified JSON containing the predicted features vector of the given image.

</td>
</tr>
</table>

