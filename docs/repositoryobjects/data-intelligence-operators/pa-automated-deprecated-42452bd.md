<!-- loio42452bd27c544ec6bfc0e56ceab4d8eb -->

# PA Automated \(Deprecated\)

This operator applies the PA Automed Analytics product for prediction of values. Note that a pre-trained model for PA Automed Analytics must exist and reside in a folder relative to the `<VFLOW_REPO>/blobs` directory.



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loio42452bd27c544ec6bfc0e56ceab4d8eb__section_sq1_nf3_vdb"/>

## Configuration Parameters


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

`modelPath` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Contains the path relative to `<VFLOW_REPO>/blobs/` where the kxen models are stored, for example, the KxAdmin.txt file and the model files.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

`modelName` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The name of the model that should be deployed. Must be contained in the KxAdmin.txt file, otherwise the operator will fail.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

`operatingMode` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Operating mode that is either `stream` or `resultfile`.

Default: "stream"

</td>
</tr>
<tr>
<td valign="top">

`schemaDescFile` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Kxen-schema description file for the incoming strings or CSV input file.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

`streamCacheSize` 

</td>
<td valign="top">

integer

</td>
<td valign="top">

If in stream mode, this specifies the size of the internal stream chunk cache.

Default: 10000

</td>
</tr>
</table>



<a name="loio42452bd27c544ec6bfc0e56ceab4d8eb__section_knq_5f3_vdb"/>

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

`inDataCSVPath` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Local path of the input data CSV file.

</td>
</tr>
<tr>
<td valign="top">

`inData` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Input port for streaming data.

</td>
</tr>
</table>



<a name="loio42452bd27c544ec6bfc0e56ceab4d8eb__section_swc_cg3_vdb"/>

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

`outResultContent` 

</td>
<td valign="top">

string

</td>
<td valign="top">

If operatingMode is "stream", this port streams the result line by line. If the operatingMode is "resultfile", the output will be the filepath to the result file.

</td>
</tr>
</table>

