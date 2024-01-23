<!-- loio40c0ec97682e481e90d4834832c92bb4 -->

# Data Transfer

The Data Transfer operator helps transfer data from an SAP Business Warehouse system to major cloud storage such as Amazon Simple Storage Service, Microsoft Azure Data Lake, Alibaba Cloud Object Storage Service, Google Cloud Storage, Microsoft Azure Storage Blob, or Hadoop Distributed File System.



This operator enables you to select the source data from an SAP BW system and the target storage to which you want to transfer the data. It has one input port \(`input`\) and two output ports \(`output` and `error`\). Use this operator in a graph that uses only other data workflow operators.



Connect the input port to another data workflow operator to trigger its start. On the `error` output port, the engine writes a message in case of errors when trying to execute the data transfer. On success, the engine writes a message on the `output` port. If you want the execution of the graph to proceed, connect the respective output ports to other data workflow operators.

> ### Note:  
> Any message written to an unconnected output port results in a graph failure.



<a name="loio40c0ec97682e481e90d4834832c92bb4__section_sq1_nf3_vdb"/>

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

source

</td>
<td valign="top">

custom

</td>
<td valign="top">

-   Source SAP BW system and a data source \(BW query or BW InfoProvider\) within the system.
-   Variable values, if any.



</td>
</tr>
<tr>
<td valign="top">

target

</td>
<td valign="top">

custom

</td>
<td valign="top">

Target cloud storages.

</td>
</tr>
</table>



<a name="loio40c0ec97682e481e90d4834832c92bb4__section_knq_5f3_vdb"/>

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



<a name="loio40c0ec97682e481e90d4834832c92bb4__section_swc_cg3_vdb"/>

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



For more information about using the Data Transfer operator, see [Transfer Data from SAP BW to Cloud Storage](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/3b100723393b4a7d85e5c840f970550b.html "Use the Data Transfer operator in a data workflow graph (pipeline) to transfer data from an SAP Business Warehouse (BW) system to cloud storage.") :arrow_upper_right:.

