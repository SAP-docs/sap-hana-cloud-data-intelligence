<!-- loio4525f87d7ed44b22af05693296d33a17 -->

# Pipeline

Pipeline operator helps execute an SAP Data Intelligence pipeline in an SAP Data Intelligence system.



> ### Note:  
> This operator's external connection feature will be deprecated and should no longer be considered. For secure external graph connections, such as start of external graphs, the following API is recommended: `POST - /v1/runtime/graphs`.
> 
> More API details are available here:
> 
> [https://api.sap.com/api/vflow/resource](https://api.sap.com/api/vflow/resource)

The data pipeline, when executed, can help process the raw data from multiple sources and make it available for different use cases.



This operator has one input port, Input, and two output ports, Output and Error. Use this operator in a graph that uses only other data workflow operators.

Connect the input port to another data workflow operator to trigger its start. On the Error output port, the engine writes a message in case of errors when trying to execute the Pipeline. On success, the engine writes a message on the Output port. If you want the execution of the graph to proceed, connect the respective output ports to other data workflow operators.

> ### Note:  
> Any message written to an unconnected output port results in a graph failure.



<a name="loio4525f87d7ed44b22af05693296d33a17__section_sq1_nf3_vdb"/>

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

VFlow Connection

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

Graph Name

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the graph to execute.

> ### Note:  
> The value help that the tool provides lists only the graphs from the local instance \( \(that is, the currently used modeler instance\) even if you have selected a remote instance.



</td>
</tr>
<tr>
<td valign="top">

Running Permanently

</td>
<td valign="top">

string

</td>
<td valign="top">

If set to *true*, the operator execution checks whether the data pipeline state is in a running state. Then it starts the data pipeline execution if it is not in a running state, and terminates immediately \(status: completed\) while the data pipeline remains in the running state. But, if the task was already running with a different task version, then that instance is stopped, and the new task version is started and immediately terminated \(status: completed\).

If set to *false*, the operator executes the data pipeline once, and the operator execution terminates after the pipeline execution terminates.

> ### Remember:  
> If you do not provide any value, the modeler uses `false` as the default value.



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

Maximum number of attempts \(default 10\) to query for a status update.

</td>
</tr>
</table>



<a name="loio4525f87d7ed44b22af05693296d33a17__section_v3m_jcw_k2b"/>

## Configuration Parameters \(manual\)

If you are manually entering the connection details of the SAP Data Intelligence system in which you want to execute the pipeline:


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

Host name of the Modeler system. For example, `localhost`.

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

"HTTPS" or "HTTP"

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

Name of the user used for the authentication. Use this syntax, `tenant\username`.

`tenant` is the tenant to use and `username` the login user name.

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

The password of the user used for the authentication.

</td>
</tr>
</table>



<a name="loio4525f87d7ed44b22af05693296d33a17__section_knq_5f3_vdb"/>

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

Accepts a message from a connected data workflow operator.

</td>
</tr>
</table>



<a name="loio4525f87d7ed44b22af05693296d33a17__section_swc_cg3_vdb"/>

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

If the operator executed successfully, this port transports the success message.

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

Operator error. If the port is connected then the graph will keep running. If it is not connected, the graph will terminate with the operator error.

</td>
</tr>
</table>



For more information, see [Run an SAP Data Intelligence Pipeline](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/69bbcf990caa4439b24515dd02b42918.html "Use the Pipeline operator in the SAP Data Intelligence Modeler application to run (execute) a graph (pipeline) in an SAP Data Intelligence system.") :arrow_upper_right:.

