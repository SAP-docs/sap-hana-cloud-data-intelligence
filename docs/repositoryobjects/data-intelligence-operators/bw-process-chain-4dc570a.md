<!-- loio4dc570a257444a34ad0b7c9b6cceb875 -->

# BW Process Chain

The BW Process Chain operator helps execute an SAP BW process chain in an SAP BW system.



SAP BW process chain is a sequence of processes that are scheduled to wait in the background for an event. Some of these processes can trigger a separate event that can, in turn, start other processes.



This operator has one input port \(`input`\) and two output ports \(`output` and `error`\). Use this operator in a graph that uses only other data workflow operators.

Connect the input port to another data workflow operator to trigger its start. On the `error` output port, the engine writes a message in case of errors when trying to execute the process chain. On success, the engine writes a message on the `output` port. If you want the execution of the graph to proceed, connect the respective output ports to other data workflow operators.

> ### Note:  
> Any message written to an unconnected output port results in the graph failure.



<a name="loio4dc570a257444a34ad0b7c9b6cceb875__section_sq1_nf3_vdb"/>

## Configuration Parameters \(using Connection ID\)


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

SAP BW Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Connection ID that references a connection to a remote SAP Data Intelligence system.

</td>
</tr>
<tr>
<td valign="top">

SAP BW ProcessChain ID

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the process chain to execute

</td>
</tr>
<tr>
<td valign="top">

Retry Interval

</td>
<td valign="top">

string

</td>
<td valign="top">

Time interval in seconds \(default 20\) to wait until next status update.

</td>
</tr>
<tr>
<td valign="top">

Retry Attempts

</td>
<td valign="top">

string

</td>
<td valign="top">

Maximum number of attempts \(default 1080\) to query for status update.

</td>
</tr>
</table>



<a name="loio4dc570a257444a34ad0b7c9b6cceb875__section_v3m_jcw_k2b"/>

## Configuration Parameters \(manual\)

If you are manually entering the connection details of the SAP BW system in which you want to execute the process chain:


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

Host

</td>
<td valign="top">

string

</td>
<td valign="top">

Host name of the SAP BW system. For example, `host.name`.

</td>
</tr>
<tr>
<td valign="top">

Port

</td>
<td valign="top">

number

</td>
<td valign="top">

Port number. For example, `8090`.

</td>
</tr>
<tr>
<td valign="top">

Protocol

</td>
<td valign="top">

string

</td>
<td valign="top">

"HTTPS" or "HTTP".

</td>
</tr>
<tr>
<td valign="top">

User

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the user for the authentication.

</td>
</tr>
<tr>
<td valign="top">

Password

</td>
<td valign="top">

string

</td>
<td valign="top">

Password for authentication.

</td>
</tr>
</table>



<a name="loio4dc570a257444a34ad0b7c9b6cceb875__section_knq_5f3_vdb"/>

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

Accepts message from a connected data workflow operator.

</td>
</tr>
</table>



<a name="loio4dc570a257444a34ad0b7c9b6cceb875__section_swc_cg3_vdb"/>

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

If the operator executed successfully, this port carries the success message.

</td>
</tr>
<tr>
<td valign="top">

`error` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Operator error. If the port is connected, then the graph will keep running. If it is not connected, the graph will terminate with the operator error.

</td>
</tr>
</table>



For more information on how to use this operator, see [Run an SAP BW Process Chain Operator](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/dd9357c7f5e34a3ea9a0607f0b8f2e56.html "To run (execute) an SAP Business Warehouse (BW) process chain in an SAP BW system, use the BW Process Chain operator in the SAP Data Intelligence Modeler application.") :arrow_upper_right:.

