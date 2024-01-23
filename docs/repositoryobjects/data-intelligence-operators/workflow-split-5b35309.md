<!-- loio5b353094d36a4bb8960fc22a49326890 -->

# Workflow Split

The Workflow Split operator helps duplicate an input message into two output messages.



The Workflow Split operator is intended to control the flow of execution when there are parallel executions within the graph. The operator has one input port and two output ports. The operator sends the message at the input port to both the output ports.



<a name="loio5b353094d36a4bb8960fc22a49326890__section_ufc_dzc_l2b"/>

## Configuration Parameters

None



<a name="loio5b353094d36a4bb8960fc22a49326890__section_swc_cg3_vdb"/>

## Input


<table>
<tr>
<th valign="top">

Iutput

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

`in` 

</td>
<td valign="top">

any.\*

</td>
<td valign="top">

Accepts a message from the connected data workflow operator.

</td>
</tr>
</table>



<a name="loio5b353094d36a4bb8960fc22a49326890__section_knq_5f3_vdb"/>

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

`out1` 

</td>
<td valign="top">

any.\*

</td>
<td valign="top">

Sends the incoming message to another connected data workflow operator.

</td>
</tr>
<tr>
<td valign="top">

`out2` 

</td>
<td valign="top">

any.\*

</td>
<td valign="top">

Sends the incoming message to another connected data workflow operator.

</td>
</tr>
</table>

> ### Note:  
> Leaving the output port unconnected results in a graph failure when the operator receives an input message.



For an example on how to use the Workflow Split \(and\) operator, see [Control Flow of Execution](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/c7723e3a10f94a74b15f925b3d9eeda5.html "SAP Data Intelligence provides the data workflow operators Workflow Merge (or), Workflow Merge (and), and Workflow Split to control the flow of execution in a data workflow.") :arrow_upper_right:.

