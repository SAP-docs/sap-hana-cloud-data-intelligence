<!-- loio327ec61fb1e9475996630a73575aea76 -->

# Topic Detection \(Deprecated\)

A functional service for detecting and ranking topics from documents. Extracted keywords from provided documents are based on Non-negative Matrix Factorization \(NMF\).



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loio327ec61fb1e9475996630a73575aea76__section_bry_smn_b3b"/>

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

optionsTopic

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. Object that must be configured with the parameter fields that follow.

</td>
</tr>
<tr>
<td valign="top">

Number of Topics

</td>
<td valign="top">

numTopics

</td>
<td valign="top">

int

</td>
<td valign="top">

Mandatory. Total number of topics to be detected

Default: 20

</td>
</tr>
<tr>
<td valign="top">

Number of Topics per Document

</td>
<td valign="top">

numTopicsPerDoc

</td>
<td valign="top">

int

</td>
<td valign="top">

Mandatory. Number of most relevant topics to be listed per document

Default: 1

</td>
</tr>
<tr>
<td valign="top">

Number of Keywords per Topic

</td>
<td valign="top">

numKeywordsPerTopic

</td>
<td valign="top">

int

</td>
<td valign="top">

Mandatory. Number of keywords to be listed per topic

Default: 15

</td>
</tr>
<tr>
<td valign="top">

Number of Features

</td>
<td valign="top">

numFeatures

</td>
<td valign="top">

int

</td>
<td valign="top">

Maximum number of keywords to be extracted from documents in total

</td>
</tr>
</table>



<a name="loio327ec61fb1e9475996630a73575aea76__section_zgh_xbg_b3b"/>

## Input


<table>
<tr>
<th valign="top">

Parameter

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

A message whose body is the input information sent to the service. The header can optionally set the configuration parameters. Configuration parameters can be either set from this message header or from the configuration dialog of the operator. If at least one configuration parameter is set in the message header then the parameters from the configuration dialog are ignored. The input files need to be raw text format. At least two documents must be submitted. The documents need to be wrapped in an archive file. Accepted file extensions: zip, tar, gz, or tgz.

</td>
</tr>
</table>

The archive file path can be passed in the message body. For example:


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

And with the same configuration parameters:


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

\{"options": \{"numTopics":20, "numTopicsPerDoc":1, "numKeywordsPerTopic":15\}\}

</td>
<td valign="top">

"/path/to/file/sample.zip"

</td>
</tr>
</table>

Alternatively, the file content of the input archive can be passed as blob in the message body. In this case, it is required to include the file name as an attribute with name storage.filename. For example, together with the optional configuration parameters:


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

\{"storage.filename": "/path/to/file/sample.zip", "options": \{"numTopics":20, "numTopicsPerDoc":1, "numKeywordsPerTopic":15\}\}

</td>
<td valign="top">

Serialized file as blob.

</td>
</tr>
</table>



<a name="loio327ec61fb1e9475996630a73575aea76__section_kdn_2cg_b3b"/>

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

The inference result as a JSON string. For each input document the detected topic IDs are listed. And for each detected topic its score and keywords are listed, per document.

</td>
</tr>
</table>

Example:

```
{
  "_id": "402a582a-c18e-4466-b8c0-085f5c244da6",
  "predictions": [
    {
      "docName": "doc1",
      "topics": [
        0,
        6
      ],
      "scores": [
        0.14,
        0.15
      ],
      "keywords": [
        [
          "kw1",
          "kw2",
          "kw3"
        ],
        [
          "kw10",
          "kw21",
          "kw32"
        ]
      ]
    },...
  ],
  "request": {
    "files": [
      "sample.zip"
    ],
    "options": {
      "numTopics": 3,
      "numTopicsPerDoc": 2,
      "numKeywordsPerTopic": 4,
      "numFeatures": 100
    }
  },
  "status": "DONE"
}
```

**Error**: If an error happens due to an input, this port outputs a message. If this port is not connected, a failure will stop the graph with an error.

**Related Information**  


[Topic Detection](topic-detection-df20169.md "")

