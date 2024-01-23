<!-- loio8084d07ad18c47df926a1d0dec856c47 -->

# Workflow Trigger and Workflow Terminator

The operators *Workflow Trigger* and *Workflow Terminator* control the beginning and ending of a data workflow graph \(pipeline\).

Use the *Workflow Trigger* and *Workflow Terminator* operators only with the other operators in the Data Workflow category. The following table contains descriptions for each operator.


<table>
<tr>
<th valign="top">

Operator

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

*Workflow Trigger* 

</td>
<td valign="top">

Sends a start message to the next operator in the graph, which starts the data workflow graph. The *Workflow Trigger* operator has one output port; it doesn't have an input port.

Once the graph run is started, the *Workflow Trigger* operator sends a message to its output port. If the output port is connected to another Data Workflow operator, the next operator starts its execution. However, if the *Workflow Trigger* output port isn't connected to a Data Workflow operator, the execution of the data workflow graph fails.

</td>
</tr>
<tr>
<td valign="top">

*Workflow Terminator* 

</td>
<td valign="top">

Shuts down, or terminates, the execution of the data workflow graph. The *Workflow Terminator* operator has one input port; it doesn't have an output port.

Once the *Workflow Terminator* receives a message from the upstream operator to its input port, it terminates the data workflow graph with the state, *Completed*.

</td>
</tr>
</table>

