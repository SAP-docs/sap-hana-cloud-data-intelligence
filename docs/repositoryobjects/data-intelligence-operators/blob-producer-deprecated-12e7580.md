<!-- loio12e7580aa8c84fc981e8beea31d395b8 -->

# Blob Producer \(Deprecated\)

The Blob Producer operator is to push a blob to the blob repository.



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loio12e7580aa8c84fc981e8beea31d395b8__section_sq1_nf3_vdb"/>

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

versionControl

</td>
<td valign="top">

string

</td>
<td valign="top">

Operation mode of the operator. If its value is 'conf' the blob name and blobVersion are taken form the configuration parameters. If its value is 'input' the blob name and blob version is taken from the input ports. "auto" mode is defined to increase the blob version automatically by the operator. It takes the blobVersion parameter as the prefix of the blob version and pushes blob with version appending a number to this prefix. The version number is in increasing order and starts from 1. If there is a blob in the repository with the given name, it takes the version number of the latest version with this version prefix as starting version number.

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

The name of the blob to be produced. This configuration parameter is used only in 'conf' and 'auto' modes.

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

The version of the blob to be produced. This configuration parameter is used only in 'conf' and 'auto' modes.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

blobType

</td>
<td valign="top">

string

</td>
<td valign="top">

The type of the blob to be produced. This configuration parameter is used only in 'conf' and 'auto' modes.

Default: "object"

</td>
</tr>
</table>



<a name="loio12e7580aa8c84fc981e8beea31d395b8__section_knq_5f3_vdb"/>

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

The name of the blob to push to the repository. Used only in 'input' mode.

Default:

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

The version of the blob to push to the repository. Used only in 'input' mode.

Default:

</td>
</tr>
<tr>
<td valign="top">

`inBlobMetadata` 

</td>
<td valign="top">

string

</td>
<td valign="top">

The metadata of the blob to push to the repository.

Default:

</td>
</tr>
<tr>
<td valign="top">

`inBlobPath` 

</td>
<td valign="top">

string

</td>
<td valign="top">

The path of the blob to push to the repository. The content of this port is not used if the blob binary has already been supplied.

</td>
</tr>
<tr>
<td valign="top">

`inBlobBinary` 

</td>
<td valign="top">

blob

</td>
<td valign="top">

The binary of the blob to push to the repository. The content of this port is not used if the blob path has already been supplied.

</td>
</tr>
</table>



<a name="loio12e7580aa8c84fc981e8beea31d395b8__section_swc_cg3_vdb"/>

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

`success` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Output to indicate the blob is pushed to the repository successfully.

</td>
</tr>
</table>

