<!-- loio6be13b9fab3944be8eef2dc4fa327229 -->

# Workflow Merge \(or\)

The Workflow Merge \(or\) operator helps control the flow of execution in a data workflow.



This operator sends a message to the output port once it receives a message from any of the input ports. All further inputs are ignored.



<a name="loio6be13b9fab3944be8eef2dc4fa327229__section_ufc_dzc_l2b"/>

## Configuration Parameters

None



<a name="loio6be13b9fab3944be8eef2dc4fa327229__section_knq_5f3_vdb"/>

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

`input` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Accepts message from another data workflow operator.

</td>
</tr>
<tr>
<td valign="top">

`input2` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Accepts message from another data workflow operator.

</td>
</tr>
</table>

> ### Note:  
> If the input ports are connected to other data workflow operators and if the operator receives a message at any of its input ports, then leaving the output port unconnected results in a data workflow execution failure.



<a name="loio6be13b9fab3944be8eef2dc4fa327229__section_swc_cg3_vdb"/>

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

`output` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Message from the operator once it receives a message from any of its input ports.

</td>
</tr>
</table>

For an example on how to use the Workflow Merge \(or\) operator, see [Control Flow of Execution](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/c7723e3a10f94a74b15f925b3d9eeda5.html "SAP Data Intelligence provides the data workflow operators Workflow Merge (or), Workflow Merge (and), and Workflow Split to control the flow of execution in a data workflow.") :arrow_upper_right:.

