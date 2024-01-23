<!-- loio539680c2cffa47f6b744d113eb848a3d -->

# SAP Data Services Job

The SAP Data Services Job operator helps run an SAP Data Services job in a remote system.



Running an SAP Data Services job helps users to integrate, transform, and improve the data quality.



This operator has one input port, Input, and two output ports, Output and Error. Use this operator in a graph that uses only other data workflow operators.

Connect the input port to another data workflow operator to trigger its start. On the Error output port, the engine writes a message of errors when trying to execute the job. On success, the engine writes a message on the Output port. If you want the execution of the graph to proceed, connect the respective output ports to other data workflow operators.

> ### Note:  
> Any message written to an unconnected output port results in a graph failure.



<a name="loio539680c2cffa47f6b744d113eb848a3d__section_sq1_nf3_vdb"/>

## Configuration Parameters


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

Repository name

</td>
<td valign="top">

string

</td>
<td valign="top">

Remote Data Services repository name.

</td>
</tr>
<tr>
<td valign="top">

Job

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the remote SAP Data Services job.

</td>
</tr>
<tr>
<td valign="top">

Job server name

</td>
<td valign="top">

string

</td>
<td valign="top">

Remote Data Services job server name.

</td>
</tr>
<tr>
<td valign="top">

Job server type

</td>
<td valign="top">

string

</td>
<td valign="top">

Remote Data Services job server type \[JOBSERVER | SERVERGROUP\]

</td>
</tr>
<tr>
<td valign="top">

Distribution Level

</td>
<td valign="top">

string

</td>
<td valign="top">

Remote Data Services job execution distribution level \[Job | Dataflow | Subdataflow\]

</td>
</tr>
<tr>
<td valign="top">

System Configuration

</td>
<td valign="top">

string

</td>
<td valign="top">

Remote Data Services system configuration that is used to execute the job. It may be production system, QA system, or development system.

</td>
</tr>
<tr>
<td valign="top">

Global Variables

</td>
<td valign="top">

array

</td>
<td valign="top">

Remote Data Services job global variables runtime values.

</td>
</tr>
<tr>
<td valign="top">

Substitution Parameters

</td>
<td valign="top">

array

</td>
<td valign="top">

Remote Data Services job substitution parameters runtime values.

</td>
</tr>
</table>



<a name="loio539680c2cffa47f6b744d113eb848a3d__section_knq_5f3_vdb"/>

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

`in`

</td>
<td valign="top">

string

</td>
<td valign="top">

Trigger job processing.

</td>
</tr>
</table>



<a name="loio539680c2cffa47f6b744d113eb848a3d__section_swc_cg3_vdb"/>

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

`outsuccess`

</td>
<td valign="top">

string

</td>
<td valign="top">

Success output of remote task.

</td>
</tr>
<tr>
<td valign="top">

`outError`

</td>
<td valign="top">

string

</td>
<td valign="top">

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph ends with the operator error.

</td>
</tr>
</table>

> ### Note:  
> This operator requires workflow trigger input to start in a graph and workflow terminator to stop. Without trigger input or workflow terminator, the graph appears to be running forever.



For more information, see [Run an SAP Data Intelligence Pipeline](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/69bbcf990caa4439b24515dd02b42918.html "Use the Pipeline operator in the SAP Data Intelligence Modeler application to run (execute) a graph (pipeline) in an SAP Data Intelligence system.") :arrow_upper_right:.

