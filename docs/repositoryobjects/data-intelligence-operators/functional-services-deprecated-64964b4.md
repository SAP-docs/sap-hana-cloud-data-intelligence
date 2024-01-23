<!-- loio64964b493d5e48aba3fcd5d192d63463 -->

# Functional Services \(Deprecated\)

This operator gives you access to pretrained functional services based on Machine Learning.



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

> ### Note:  
> Functional services are available only on AWS.

Supported services are:

-   [Image Classification \(Deprecated\)](image-classification-deprecated-558c6ae.md)

-   [Image Feature Extraction \(Deprecated\)](image-feature-extraction-deprecated-60b4c9b.md)

-   [Image OCR \(Deprecated\)](image-ocr-deprecated-046d8c4.md)

-   [Similarity Scoring \(Deprecated\)](similarity-scoring-deprecated-2cdc58f.md)

-   [Text Classifier \(Deprecated\)](text-classifier-deprecated-2a8c5e2.md)

-   [Topic Detection \(Deprecated\)](topic-detection-deprecated-327ec61.md)




## Configuration Parameters

Choose the desired functional service with the configuration option `Functional Service`. Depending on which service is chosen, certain configuration options are displayed.

These service-specific configuration parameters can be either set in the configuration dialog or as part of the input data to the service operator. The description of the configuration options as well as the input and output data can be found in the documentation for the respective service by selecting the name of the functional service below.

All services require a connection to ML Foundation. There are four options for setting the connection in the configuration parameter `ML Connection`:


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

ML Connection

</td>
<td valign="top">

mlAPIConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Information about connection to ML Foundation.

</td>
</tr>
<tr>
<td valign="top">

ML Default

</td>
<td valign="top">



</td>
<td valign="top">



</td>
<td valign="top">

The URLs and credentials. If you do not know what connection to choose this is probably the right choice for you.

</td>
</tr>
<tr>
<td valign="top">

HTTP Connection

</td>
<td valign="top">



</td>
<td valign="top">



</td>
<td valign="top">

Connections of this type need to have URLs and credentials set in the Connection Management app.

</td>
</tr>
<tr>
<td valign="top">

HTTP Connection ID

</td>
<td valign="top">

httpConnectionID

</td>
<td valign="top">

string

</td>
<td valign="top">

The ID of the connection information to retrieve from the Connection Management Service.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

ML Cluster Connection

</td>
<td valign="top">



</td>
<td valign="top">



</td>
<td valign="top">

Connections of this type will already have all information defined in the Connection Management app.

</td>
</tr>
<tr>
<td valign="top">

Connection ID

</td>
<td valign="top">

connectionID

</td>
<td valign="top">

string

</td>
<td valign="top">

The ID of the connection information to retrieve from the Connection Management Service.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Manual

</td>
<td valign="top">



</td>
<td valign="top">



</td>
<td valign="top">

A custom connection requiring all specific fields to be filled.

</td>
</tr>
</table>

-   **[Image Classification \(Deprecated\)](image-classification-deprecated-558c6ae.md "This is a pretrained image classification service. The model for the classifier was
		obtained by training on the ILSVRC2014 Task 2 dataset. The service takes as input one or
		several images and classifies each of them into a set of 1000 categories such as trees,
		animals, food, vehicles, people, and more.")**  
This is a pretrained image classification service. The model for the classifier was obtained by training on the ILSVRC2014 Task 2 dataset. The service takes as input one or several images and classifies each of them into a set of 1000 categories such as trees, animals, food, vehicles, people, and more.
-   **[Image Feature Extraction \(Deprecated\)](image-feature-extraction-deprecated-60b4c9b.md "A functional service for extracting image features, one vector for each input image. The
		vectors can be used for comparison, information retrieval, clustering, or further
		processing. ")**  
A functional service for extracting image features, one vector for each input image. The vectors can be used for comparison, information retrieval, clustering, or further processing.
-   **[Image OCR \(Deprecated\)](image-ocr-deprecated-046d8c4.md "The inference service for Optical Character Recognition (OCR) takes an image or PDF file
		as input and outputs the recognized text from the image (or PDF).")**  
The inference service for Optical Character Recognition \(OCR\) takes an image or PDF file as input and outputs the recognized text from the image \(or PDF\).
-   **[Similarity Scoring \(Deprecated\)](similarity-scoring-deprecated-2cdc58f.md "A functional service for comparing vectors using a similarity score ranging from -1 to 1
		(larger values mean a high similarity).")**  
A functional service for comparing vectors using a similarity score ranging from -1 to 1 \(larger values mean a high similarity\).
-   **[Text Classifier \(Deprecated\)](text-classifier-deprecated-2a8c5e2.md "This is a pre-trained text classification service. ")**  
This is a pre-trained text classification service.
-   **[Topic Detection \(Deprecated\)](topic-detection-deprecated-327ec61.md "A functional service for detecting and ranking topics from documents. Extracted keywords
		from provided documents are based on Non-negative Matrix Factorization (NMF).")**  
A functional service for detecting and ranking topics from documents. Extracted keywords from provided documents are based on Non-negative Matrix Factorization \(NMF\).

