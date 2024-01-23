<!-- loio5f546d042eac42589bb95a4974eb7b3f -->

# Blob Consumer \(Deprecated\)

The Blob Consumer operator is to consume a blob in the blob repository. It can take the blob name and blob version either from input port \('input' mode\) or configuration \('conf' mode\) and give the path of the blob as its output.



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loio5f546d042eac42589bb95a4974eb7b3f__section_sq1_nf3_vdb"/>

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

opMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Operation mode of the operator. If its value is 'conf' the blob with blobName and blobVersion written in the configuration parameters is served. If its value is 'input' the blob name and blob version is taken from the input ports.

Default: "conf"

</td>
</tr>
<tr>
<td valign="top">

blobName

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the blob to be consumed. This configuration parameter is used only in 'conf' mode.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

blobVersion

</td>
<td valign="top">

string

</td>
<td valign="top">

The version of the blob to be consumed. This configuration parameter is used only in 'conf' mode.

Default: "latest"

</td>
</tr>
<tr>
<td valign="top">

perodicy

</td>
<td valign="top">

string

</td>
<td valign="top">

Specifies whether blob is sent only once or in periodic intervals..

Default: ""

</td>
</tr>
<tr>
<td valign="top">

intervalInMs

</td>
<td valign="top">

string

</td>
<td valign="top">

If periodicy is set to 'interval', then 'intervalInMS' specifies the interval period.

Default: ""

</td>
</tr>
</table>



<a name="loio5f546d042eac42589bb95a4974eb7b3f__section_knq_5f3_vdb"/>

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

`inBlobName` 

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the blob to be consumed. This port only in 'input' mode.

</td>
</tr>
<tr>
<td valign="top">

`inBlobVersion` 

</td>
<td valign="top">

string

</td>
<td valign="top">

The version of the blob to be consumed. This port only in 'input' mode.

</td>
</tr>
</table>



<a name="loio5f546d042eac42589bb95a4974eb7b3f__section_swc_cg3_vdb"/>

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

`outBlobPath` 

</td>
<td valign="top">

string

</td>
<td valign="top">

The path of the consumed blob in the blob repository.

</td>
</tr>
<tr>
<td valign="top">

`outBlob` 

</td>
<td valign="top">

blob

</td>
<td valign="top">

The actual binary.

</td>
</tr>
<tr>
<td valign="top">

`outMetadata` 

</td>
<td valign="top">

string

</td>
<td valign="top">

The metadata map \(stringified JSON object\).

</td>
</tr>
</table>

