<!-- loio60b4c9bcc35a4d408377f500d47ad690 -->

# Image Feature Extraction \(Deprecated\)

A functional service for extracting image features, one vector for each input image. The vectors can be used for comparison, information retrieval, clustering, or further processing.



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loio60b4c9bcc35a4d408377f500d47ad690__section_zgh_xbg_b3b"/>

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

A message that contains the input data to the service.

</td>
</tr>
</table>

The body of the message can be one of the following:


<table>
<tr>
<th valign="top">

Message Body

</th>
<th valign="top">

Header

</th>
<th valign="top">

Body

</th>
</tr>
<tr>
<td valign="top">

A path to an input image \(supported are: jpg, jpe, jpeg, png, gif, bmp, tif, or tiff\). The header is ignored in this case.

</td>
<td valign="top">

\{\}

</td>
<td valign="top">

/home/test/sample.jpg

</td>
</tr>
<tr>
<td valign="top">

A path to an archive containing several image files \(supported are: zip, tar, gz, tgz\). The header is ignored in this case.

</td>
<td valign="top">

\{\}

</td>
<td valign="top">

/home/test/sample.zip

</td>
</tr>
<tr>
<td valign="top">

A blob containing the input image or input archive \(for supported formats, see above\). In this case it is required to include the file name as an attribute with name storage.filename in the header.

</td>
<td valign="top">

\{"storage.filename": "/home/test/sample.jpg"\}

</td>
<td valign="top">

Serialized file as blob.

</td>
</tr>
</table>

You can directly wire the outFile port from the Read File operator to the input port of this operator.



<a name="loio60b4c9bcc35a4d408377f500d47ad690__section_kdn_2cg_b3b"/>

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

The inference result as a JSON string, the format varies according to the service.

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
      "featureVectors": [
        1.5959638357162476,...
      ]
    },
    {
      "name": "image2.jpg",
      "featureVectors": [
        0.20161056518554688,...
      ]
    }
  ],
  "processedTime": "2017-10-06T10:21:33.575961",
  "status": "DONE"
}
```

**Error**: Ifan error happens due to an input, this port outputs a message. If this port is not connected, a failure will stop the graph with an error.

**Related Information**  


[Image Feature Extraction](image-feature-extraction-c964cda.md "")

