<!-- loio2cdc58fdd0a74a8687bb0ebeacdf07fd -->

# Similarity Scoring \(Deprecated\)

A functional service for comparing vectors using a similarity score ranging from -1 to 1 \(larger values mean a high similarity\).



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



The similarity score is calculated based on the cosine similarity of the vectors. The vectors are ranked by similarity and the IDs of the top n similar vectors are listed in the output together with their similarity score. The vectors retrieved from the “image feature extraction” service can be used as input to this service.



<a name="loio2cdc58fdd0a74a8687bb0ebeacdf07fd__section_l3r_ldg_b3b"/>

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

Options

</td>
<td valign="top">

optionsSim

</td>
<td valign="top">

object

</td>
<td valign="top">



</td>
</tr>
<tr>
<td valign="top">

Number of Similar Vectors

</td>
<td valign="top">

numSimilarVectors

</td>
<td valign="top">

int

</td>
<td valign="top">

Number of most similar vectors to return in response.

</td>
</tr>
</table>



<a name="loio2cdc58fdd0a74a8687bb0ebeacdf07fd__section_zgh_xbg_b3b"/>

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

A message whose body is the input information sent to the service. The numSimilarVectors parameter needs to be set either in the configuration dialog of the operator or in the header of the input message.

</td>
</tr>
</table>

The input vectors for the service can be provided in three different format options. These input formats cannot be mixed. By default, all vectors in the input will be compared to each other \(all pairwise combinations\). The third input format also allows to define a "query set".



### Format Options

-   A path to an archive file containing the input vectors can be passed in the message body. Accepted file extensions or formats: zip, tar, gz or tgz. The archive needs to contain one file for each input vector. The file extension should be .txt with the following format \[number, number, number, …, number\]. All values in one line.

    **Examples of input message type files:**


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
    
    \{"options": \{"numSimilarVectors":1\}\}
    
    </td>
    <td valign="top">
    
    /home/test/sample.zip
    
    </td>
    </tr>
    </table>
    
-   The archive \(with the same format as described above\) can be sent as blob in the message body. In this case it is required to include the file name as a header attribute storage.filename. For example:


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
    
    \{"storage.filename": "/path/to/file/sample.zip", "options": \{"numSimilarVectors":1\}\}
    
    </td>
    <td valign="top">
    
    Serialized file as blob.
    
    </td>
    </tr>
    </table>
    
-   The body of the message can contain the input vectors encoded as a JSON format string, which holds the set of input vectors. Each vector is represented as an object that includes two key-value pairs: ID and vector. The ID is a string, and vector is an array of numbers. The set of vectors is represented as an array of vector objects. The input JSON object should include one or two key-value pairs. If one set will be provided, the object should include one key-value pair, where key is '0’, and value is a set of vectors. In this case each vector in the set will be compared to the other vectors in this set. If two sets are provided, the object should include two key-value pairs, where the names are ‘0’ and ‘1’ and with both values being sets of vectors. In this case, for each vector from set ‘0’ top numSimilarVectors similar vectors from set ‘1’ will be found.

    **Example for one set of vectors**


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
    
    \{"options": \{"numSimilarVectors":1\}\}
    
    </td>
    <td valign="top">
    
    \{"0": \[\{"id": "v0", "vector": \[0.22, 0.93\]\}, \{"id": "v1", "vector": \[0.39, 0.69\]\}\]\}
    
    </td>
    </tr>
    </table>
    
    **Example for two sets of vectors, the first set is the "query set"**


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
    
    \{"options": \{"numSimilarVectors":1\}\}
    
    </td>
    <td valign="top">
    
    \{"0": \[\{"id": "v0", "vector": \[0.22, 0.93\]\}, \{"id": "v1", "vector": \[0.39, 0.69\]\}\], "1": \[\{"id": "u0", "vector": \[0.45, 0.12\]\}, \{"id": "u1", "vector": \[0.32, 0.68\]\}\]\}
    
    </td>
    </tr>
    </table>
    



<a name="loio2cdc58fdd0a74a8687bb0ebeacdf07fd__section_kdn_2cg_b3b"/>

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

The inference result as a JSON string.

</td>
</tr>
</table>

Example:

```
{
  "id": "f09a0cfd-e1bc-4740-5e56-919a94a56d5a",
  "predictions": [
    {
      "id": "v1",
      "similarVectors": [
        {
          "id": "v5",
          "score": 0.7713963286130165
        },...
      ]
    },
    {
      "id": "v2",
      "similarVectors": [
        {
          "id": "v10",
          "score": 0.7770760429620751
        },...
      ]
    }
  ],
  "processed_time": "2017-10-06T10:21:33.575961",
  "status": "DONE"
}
```

**Error**: If an error happens due to an input, this port outputs a message. If this port is not connected, a failure will stop the graph with an error.

**Related Information**  


[Similarity Score](similarity-score-392e0b8.md "")

