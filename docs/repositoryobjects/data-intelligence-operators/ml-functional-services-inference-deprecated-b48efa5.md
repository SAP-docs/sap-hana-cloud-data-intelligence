<!-- loiob48efa568f5342f3a02bf456ffb68b3f -->

# ML Functional Services Inference \(Deprecated\)

Prepares a request message for the Leonardo Machine Learning Foundation \(Leonardo ML Foundation\) services.



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



It should be used with `openAPI` operators \(check the example graph `com.sap.ml.leonardo.mLFFunctionalServicesInference`\). The request is a `POST` request, and it can have three input formats: `files`, `texts`, and `raw`. When the Functional Service supports more than one, the option to choose is available \(as `type`\).

For example: `Image Classification` supports only files. As the input is always a message, the body will have the data itself. More specifically, the input message body will have either a path to an image or the serialized image. Each `Functional Service` also supports a set of configurations:

-   `version`
-   `modelName`
-   `options`
-   `type`

As the inputs, the configuration also varies according to the `Functional Service`. They can also be set by the header of each input message. Given a message in the texts input port:


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

`{"options": "{"numSimilarVectors":1}"}`

</td>
<td valign="top">

`{"0": [{"id": "v0", "vector": [0.22, 0.93]}, {"id": "v1", "vector": [0.39, 0.69]}]}`

</td>
</tr>
</table>

The body will be used for the inference, and the options configuration will be set for this request as `{\"numSimilarVectors\":1}`.

For a raw input port an example would be:


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

`{}`

</td>
<td valign="top">

`"{"sourceLanguage": "en", "targetLanguages": ["de"],"units": [{"value": "It is not possible to add products to the shopping cart."}]}"`

</td>
</tr>
</table>

Finally, for files input port message and example would be:


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

`{}`

</td>
<td valign="top">

`/home/test/sample.jpg`

</td>
</tr>
</table>



<a name="loiob48efa568f5342f3a02bf456ffb68b3f__section_hxs_tmh_ghb"/>

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

Functional Services

</td>
<td valign="top">

Functional Services

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Functional service to be used \(Image Classification, Image Feature Extraction, Image OCR, Nearest Neighbor Search, Similarity Scoring, Text Classifier, Topic Detection, Translation, Translation, Scene Text Recognition\).

Default: ""

</td>
</tr>
<tr>
<td valign="top">

version

</td>
<td valign="top">

version

</td>
<td valign="top">

string

</td>
<td valign="top">

Defines which model version will be used.

Used by: Image Classification, Image Feature Extraction, Text Classifier

Default: ""

</td>
</tr>
<tr>
<td valign="top">

modelName

</td>
<td valign="top">

modelName

</td>
<td valign="top">

string

</td>
<td valign="top">

Defines which model will be used.

Used by: Image Classification, Image Feature Extraction, Text Classifier

Default: ""

</td>
</tr>
<tr>
<td valign="top">

options

</td>
<td valign="top">

options

</td>
<td valign="top">

object

</td>
<td valign="top">

Defines a JSON with the options for inference. Each functional service has its own options format and the user should correctly set it according to the documentation \(the functional service is expected to provide its own set of options\).

Used by: Image OCR, Similarity Scoring, Topic Detection

Default: ""

</td>
</tr>
<tr>
<td valign="top">

type

</td>
<td valign="top">

type

</td>
<td valign="top">

string

</td>
<td valign="top">

Defines the input format type. It is only present for services that support more than one type.

Used by: Similarity Scoring

Default: "texts"

</td>
</tr>
</table>



<a name="loiob48efa568f5342f3a02bf456ffb68b3f__section_iz1_rph_ghb"/>

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

A message whose body is the information to the POST inference request and header can set the configurations for the Functional Service. The input type can be set using the field type in the message header or configuration \(both when it is supported by the service\). They assume the following values:

-   `raw`: The body is the raw information sent to the POST inference request.

    Used by: Translation

-   `texts`: The body will be included as the values for the texts key on the form-data request.

    Used by: Text Classifier


-   `files`: The body will be included as the values for the `files` key on the form-data request.

    Used by: Image Classification, Image Feature Extraction, Image OCR, Similarity Scoring, Topic Detection, Translation, Scene Text Recognition.




</td>
</tr>
</table>



<a name="loiob48efa568f5342f3a02bf456ffb68b3f__section_il3_2rh_ghb"/>

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

