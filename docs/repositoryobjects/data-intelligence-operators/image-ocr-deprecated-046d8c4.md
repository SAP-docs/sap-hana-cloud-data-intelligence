<!-- loio046d8c4a7f164396a171d0a9722f4ad1 -->

# Image OCR \(Deprecated\)

The inference service for Optical Character Recognition \(OCR\) takes an image or PDF file as input and outputs the recognized text from the image \(or PDF\).



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loio046d8c4a7f164396a171d0a9722f4ad1__section_l3r_ldg_b3b"/>

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

options

</td>
<td valign="top">

optionsOCR

</td>
<td valign="top">

object

</td>
<td valign="top">

Object that must be configured with the following fields:

-   lang

-   outputType

-   pageSegMode

-   modeType


Default: according to parameter.

</td>
</tr>
<tr>
<td valign="top">

Languages

</td>
<td valign="top">

lang

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The language of the text submitted separated by commas. A maximum of 3 languages can be set:

-   en: English \(Default\)

-   de: German

-   fr: French

-   es: Spanish

-   ru: Russian

-   ar: Arabic

-   zh-Hans: Chinese Simplified

-   zh-Hant: Chinese Traditional

-   ja: Japanese

-   ja-vert: Japanese \(vertical text\)

-   ko: Korean

-   ko-vert: Korean \(vertical text\)

-   pt: Portuguese


Default: "en"

</td>
</tr>
<tr>
<td valign="top">

Output Type

</td>
<td valign="top">

outputType

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The output type of the result.

-   txt: plain text \(Default\)

-   xml: text with markup and additional atributes


Default: "txt"

</td>
</tr>
<tr>
<td valign="top">

Page Segmentation Mode

</td>
<td valign="top">

pageSegMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The page segmentation mode.

-   0: Orientation and script detection \(OSD\) only

-   1: Automatic page segmentation with OSD \(Default\)

-   3: Fully automatic page segmentation, but no OSD

-   4: Assume a single column of text of variable sizes

-   5: Assume a single uniform block of vertically aligned text

-   6: Assume a single uniform block of text

-   7: Treat the image as a single text line

-   8: Treat the image as a single word

-   9: Treat the image as a single word in a circle

-   10: Treat the image as a single character

-   11: Sparse text. Find as much text as possible in no particular order

-   12: Sparse text with OSD

-   13: Raw line. Treat the image as a single text line, bypassing hacks that are Tesseract-specific


Default: "1"

</td>
</tr>
<tr>
<td valign="top">

Model Type

</td>
<td valign="top">

modelType

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Type of the machine learning model for OCR.

-   lstmPrecise: precise model with LSTM cells

-   lstmFast: fast model with LSTM cells

-   lstmStandard: standard model with lstm cells \(Default\)

-   noLstm: model without LSTM cells

-   all: model with LSTM cells and standard processing algorithms


Default: "lstmStandard"

</td>
</tr>
</table>



<a name="loio046d8c4a7f164396a171d0a9722f4ad1__section_zgh_xbg_b3b"/>

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

A message whose body is the input information sent to the service. The header can optionally contain configuration parameters. Configuration parameters can be either set from this message header or from the configuration dialog of the operator. If at least one configuration parameter is set in the message header then the parameters from the configuration dialog are completely ignored. The input file can be either specified with a file path or as serialized blob in the message body. Accepted file formats or extensions: jpg, jpeg, png, pdf, or PDF.

</td>
</tr>
</table>



**Example of input message with configuration parameters and path to input file**


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

\{"options": \{"lang": "en,de", "outputType": "txt", "pageSegMode": "1", "modelType": "lstmStandard"\}\}

</td>
<td valign="top">

"/path/to/file/sample.jpg"

</td>
</tr>
</table>

For example, you could use a JS operator, enter the following script to define the input parameters and input file path, and wire this operator to the Functional Service operator:

```
$.addGenerator(gen)

function gen(ctx) {    
  var msg = {};  
  msg.Attributes = {};  
  msg.Attributes["options"] = '{"lang": ["en","de"], "outputType": "xml", "pageSegMode": "1", "modelType": "lstmStandard"}';
  msg.Body = "/path/to/file/sample.jpg"    
  $.output(msg)    
}
```

**Example for input message with input file content as blob in message body**


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

\{"storage.filename": "/path/to/file/sample.jpg", "options": \{"lang": \["en","de"\], "outputType": "txt", "pageSegMode": "1", "modelType": "lstmStandard"\}\}

</td>
<td valign="top">

Serialized file as blob.

</td>
</tr>
</table>

In this case, it is required to send the file name as an attribute with name `storage.filename`.


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

\{"storage.filename": "/home/test/sample.jpg"\}

</td>
<td valign="top">

Serialized file as blob.

</td>
</tr>
</table>

You can directly wire the outFile port from the Read File operator to the input port of this operator.



<a name="loio046d8c4a7f164396a171d0a9722f4ad1__section_kdn_2cg_b3b"/>

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
  "id": "string",
  "predictions": [
    "This is the recognized text from the input image"
  ],
  "processedTime": "string",
  "status": "DONE"
}
```

**Error**: If an error happens due to an input, this port outputs a message. If this port is not connected, a failure will stop the graph with an error.

**Related Information**  


[OCR](ocr-47a163e.md "")

