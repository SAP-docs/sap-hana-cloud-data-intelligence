<!-- loioe12de658b1a742f695e28f640c84009b -->

# Workflow Trigger

The Workflow Trigger operator sends a start message, which you can use to start a data workflow.



This operator has one output port. When started, the operator sends a message on its output port. If the output port is connected, the next data workflow operator starts its execution. But, if the output port is unconnected, the graph execution fails.

Use this operator with other data workflow operators only.



<a name="loioe12de658b1a742f695e28f640c84009b__section_sq1_nf3_vdb"/>

## Configuration Parameters

None



<a name="loioe12de658b1a742f695e28f640c84009b__section_knq_5f3_vdb"/>

## Input

None



<a name="loioe12de658b1a742f695e28f640c84009b__section_swc_cg3_vdb"/>

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

Sends a message to begin execution of the next connected data workflow operator.

</td>
</tr>
</table>

