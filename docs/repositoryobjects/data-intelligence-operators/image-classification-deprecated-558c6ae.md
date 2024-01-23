<!-- loio558c6ae5f865461a9c259f117a92edb3 -->

# Image Classification \(Deprecated\)

This is a pretrained image classification service. The model for the classifier was obtained by training on the ILSVRC2014 Task 2 dataset. The service takes as input one or several images and classifies each of them into a set of 1000 categories such as trees, animals, food, vehicles, people, and more.



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loio558c6ae5f865461a9c259f117a92edb3__section_zgh_xbg_b3b"/>

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

input

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose body is the path to the file to be classified or the path to an archive with one or several files to be classified. In this case the header is not required as there are no configuration parameters.

Accepted file extensions: zip, tar, gz, tgz, jpg, jpe, jpeg, png, gif, bmp, tif, or tiff.

</td>
</tr>
</table>

**Example of input message:**


<table>
<tr>
<th valign="top">

header

</th>
<th valign="top">

body

</th>
</tr>
<tr>
<td valign="top">

\{\}

</td>
<td valign="top">

"/path/to/file/sample.jpg"

</td>
</tr>
</table>

Or with archive:


<table>
<tr>
<th valign="top">

header

</th>
<th valign="top">

body

</th>
</tr>
<tr>
<td valign="top">

\{\}

</td>
<td valign="top">

"/path/to/file/sample.zip"

</td>
</tr>
</table>

For example, you could use a JS operator, enter the following script to define the input text, and wire this operator to the Functional Service operator:

```
$.addGenerator(gen)

function gen(ctx) {

    var msg = {};
    msg.Body = "/path/to/file/sample.jpg"
    $.output(msg)
}
```

**Example of input message with input file content as blob in message body**


<table>
<tr>
<th valign="top">

header

</th>
<th valign="top">

body

</th>
</tr>
<tr>
<td valign="top">

\{"storage.filename": "/path/to/file/sample.jpg"\}

</td>
<td valign="top">

Serialized file as blob.

</td>
</tr>
</table>

In this case it is required to send the file name as an attribute with name `storage.filename`:

You can directly wire the `outFile` port from the `Read File` operator to the input port of this operator.



<a name="loio558c6ae5f865461a9c259f117a92edb3__section_kdn_2cg_b3b"/>

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

output

</td>
<td valign="top">

message

</td>
<td valign="top">

The classification result as a JSON string. The top five categories or labels are listed together with their predicted probability, ordered by descending probability.

</td>
</tr>
</table>

Example:

```
{
  "id": "f09a0cfd-e1bc-4740-5e56-919a94a56d5a",
  "predictions": [
    {
      "name": "image1.jpg",
      "results": [
        {
          "label": "chainlink fence",
          "score": 0.71404
        },...
      ]
    },
    {
      "name": "image2.jpg",
      "results": [
        {
          "label": "spider web, spider's web",
          "score": 0.44043
        },...
      ]
    }
  ],
  "processedTime": "2017-09-29T13:38:27.729971",
  "status": "DONE"
}

```

**Related Information**  


[Image Classification](image-classification-9c2e589.md "")

