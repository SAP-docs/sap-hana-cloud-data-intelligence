<!-- loio871a5caff1fb4413b18fe89e75b84e57 -->

# Workflow Merge \(and\)

The Workflow Merge \(and\) operator helps control the flow of execution in a data workflow.



This operator sends a message to the output port when it receives a message on both input ports. The process shuts down after sending the message. This operator is intended to control the flow of execution when there are parallel executions within the data workflow.



<a name="loio871a5caff1fb4413b18fe89e75b84e57__section_ufc_dzc_l2b"/>

## Configuration Parameters

None



<a name="loio871a5caff1fb4413b18fe89e75b84e57__section_knq_5f3_vdb"/>

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
> Connect both input ports to other data workflow operators. Leaving any of the input ports unconnected results in the data workflow execution to stop.



<a name="loio871a5caff1fb4413b18fe89e75b84e57__section_swc_cg3_vdb"/>

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

Message from the operator when both its input ports receive a message.

</td>
</tr>
</table>

For an example on how to use the Workflow Merge \(and\) operator, see [Control Flow of Execution](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/c7723e3a10f94a74b15f925b3d9eeda5.html "SAP Data Intelligence provides the data workflow operators Workflow Merge (or), Workflow Merge (and), and Workflow Split to control the flow of execution in a data workflow.") :arrow_upper_right:.

