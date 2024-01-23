<!-- loio190cbc7b6d4d4d138586e2dad01ac8d6 -->

# Graph Terminator V2

The Graph Terminator operator terminates the current graph execution when all input ports receive a termination signal. This operator has only one standard input port, but you can add multiple input ports of different types according to the given termination scenario.



An input port is considered terminated if:

-   Any message is retrieved, and `On Last Batch` is set to `false`.

-   Any message received without the `com.sap.headers.batch` header.

-   A batch message with `isLast == true` in the `com.sap.headers.batch` header when `On Last Batch` is set to `true`.




<a name="loio190cbc7b6d4d4d138586e2dad01ac8d6__section_sq1_nf3_vdb"/>

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

On Last Batch

</td>
<td valign="top">

onLastBatch

</td>
<td valign="top">

bool

</td>
<td valign="top">

Mandatory. Only if you would like to terminate on a batch message even if it is not the lastBatch. Then, set this to `false`.

</td>
</tr>
</table>



<a name="loio190cbc7b6d4d4d138586e2dad01ac8d6__section_knq_5f3_vdb"/>

## Input


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

in

</td>
<td valign="top">

A generic port accepting any arbitrary incoming message.

</td>
</tr>
</table>

You can add multiple input ports of different types according to the given termination scenario where the graph should only terminate when multiple signals have been retrieved. It is important to notice that if a new port is added but it isn’t connected, the operator won’t terminate the graph since it expects all ports to be terminated before finishing the graph.



<a name="loio190cbc7b6d4d4d138586e2dad01ac8d6__section_swc_cg3_vdb"/>

## Output

None.

