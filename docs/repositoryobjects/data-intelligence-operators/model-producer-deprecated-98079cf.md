<!-- loio98079cff2c4b423390ef2f248d81f3b1 -->

# Model Producer \(Deprecated\)

The Model Producer operator is used to push a model to the model repository.



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loio98079cff2c4b423390ef2f248d81f3b1__section_sq1_nf3_vdb"/>

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

versionControl

</td>
<td valign="top">

versionControl

</td>
<td valign="top">

string

</td>
<td valign="top">

Operation mode of the operator. If its value is 'conf', the model name and modelVersion are taken from the configuration parameters. If its value is 'input', the model name and model version is taken from the input ports. "auto" mode is defined to increase the model version automatically by the operator. It takes the modelVersion parameter as the prefix of the model version and pushes model with version appending a number to this prefix. The version number is in increasing order and starts from 1. If there is a model in the repository with the given name, it takes the version number of the latest version with this version prefix as starting version number.

Default: "conf"

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

The name of the model to be consumed. This configuration parameter is used only in 'conf' and 'auto' modes.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

modelVersion

</td>
<td valign="top">

modelVersion

</td>
<td valign="top">

string

</td>
<td valign="top">

The version of the model to be consumed. This configuration parameter is used only in 'conf' and 'auto' modes.

Default: ""

</td>
</tr>
</table>



<a name="loio98079cff2c4b423390ef2f248d81f3b1__section_knq_5f3_vdb"/>

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

inModelName

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the model to push to the repository. Used only in 'input' mode.

</td>
</tr>
<tr>
<td valign="top">

inModelVersion

</td>
<td valign="top">

string

</td>
<td valign="top">

The version of the model to push to the repository. Used only in 'input' mode.

</td>
</tr>
<tr>
<td valign="top">

inModelMetadata

</td>
<td valign="top">

string

</td>
<td valign="top">

The metadata of the model to push to the repository.

</td>
</tr>
<tr>
<td valign="top">

inModelPath

</td>
<td valign="top">

string

</td>
<td valign="top">

The path of the model to push to the repository. The content of this port is not used if the model binary has already been supplied.

</td>
</tr>
<tr>
<td valign="top">

inModelBinary

</td>
<td valign="top">

string

</td>
<td valign="top">

The binary of the model to push to the repository. The content of this port is not used if the model path has already been supplied.

</td>
</tr>
</table>



<a name="loio98079cff2c4b423390ef2f248d81f3b1__section_swc_cg3_vdb"/>

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

success

</td>
<td valign="top">

string

</td>
<td valign="top">

Output to indicate that the model is pushed to the repository successfully.

</td>
</tr>
</table>

