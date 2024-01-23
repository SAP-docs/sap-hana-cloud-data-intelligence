<!-- loio9c2e589463b4421783f849ac7c560ce1 -->

# Image Classification



Uses a convolutional neural network \(CNN\) model to predict a flattened 131072 feature vector \(unflattened 2048 feature vectors of shape \(8,8\)\). Currently, the InceptionV3 model, which is pretrained on the ImageNet dataset, is used. The operator is designed to classify one image at each step. Possible input extensions are `jpg`, `jpe`, `jpeg`, `png`, `gif`, `bmp`, `tif`, and `tiff`.

> ### Note:  
> This operator is designed to work with a `readFile`-like operator, which should be connected to the `image` input port.



<a name="loio9c2e589463b4421783f849ac7c560ce1__section_vy3_zfx_v4b"/>

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



<a name="loio9c2e589463b4421783f849ac7c560ce1__section_ozm_1gx_v4b"/>

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

A stringified JSON containing the predicted class of a given image.

</td>
</tr>
</table>

**Related Information**  


[ImageNet Dataset](http://www.image-net.org)

