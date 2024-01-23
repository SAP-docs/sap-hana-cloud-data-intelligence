<!-- loio8952b8d9db9442abb30ec501bb24e1ec -->

# Workflow Terminator

The Workflow Terminator operator helps shut down the data workflow execution.



The operator has one input port. When started and when the operator receives a message, it shuts down the data workflow. The data workflow terminates with the state, *Completed*.

Use this operator with other data workflow operators only.



<a name="loio8952b8d9db9442abb30ec501bb24e1ec__section_sq1_nf3_vdb"/>

## Configuration Parameters

None



<a name="loio8952b8d9db9442abb30ec501bb24e1ec__section_swc_cg3_vdb"/>

## Input


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

Receives a message to shut down the execution of the data workflow.

</td>
</tr>
</table>



<a name="loio8952b8d9db9442abb30ec501bb24e1ec__section_knq_5f3_vdb"/>

## Output

None

