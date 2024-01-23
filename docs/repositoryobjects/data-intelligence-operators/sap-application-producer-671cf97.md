<!-- loio671cf97f398441d8bc83debae96efbea -->

# SAP Application Producer

Use the SAP Application Producer to write data to SAP and non-SAP sources as modeled in a graph. Supported in Generation 1 graphs.



This operator reads from any structured operators, and produces a table in the specified target like oData and BW.

> ### Note:  
> For BW Datastore Targets:
> 
> -   BW only supports Advanced Datastore objects as a target under the /DATASTORE folder.
> -   For BW DataStore objects as target, the option *Write Interface-Enabled* should be checked in the BW system \(under DataStore Object-\> Modeling Properties -\> Special Properties -\> \[\] Write Interface-Enabled\).
> -   To preview BW Datastore data within the operator, an ABAP connection needs to be created in the Connection Management application that is associated with the specified BW Connection. That ABAP connection then needs to be specified for the *ABAP Connection ID* field for the BW Connection.



<a name="loio671cf97f398441d8bc83debae96efbea__section_dyj_m45_fnb"/>

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

Service

</td>
<td valign="top">

String

</td>
<td valign="top">

The application where the tabular data is written

</td>
</tr>
<tr>
<td valign="top">

Connection ID

</td>
<td valign="top">

Object

</td>
<td valign="top">

Connection ID of the target system.

</td>
</tr>
<tr>
<td valign="top">

Target

</td>
<td valign="top">

Object

</td>
<td valign="top">

Remote dataset of the selected target object.

</td>
</tr>
<tr>
<td valign="top">

Maximum Batch Size

</td>
<td valign="top">

Integer

</td>
<td valign="top">

The maximum number of records from the source included in each batch. The actual number of records is automatically calculated based on the dataset definition. To disable the automatic calculation, set the *Use Defined Batch Size* option to True.

</td>
</tr>
<tr>
<td valign="top">

Use Defined Batch Size

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Set to True when the automatic calculation does not provide optimal performance. When set to True, each batch of records contains the number of records entered in the Maximum Batch Size option. For example, when Maximum Batch Size is set to 1000, and Use Defined Batch Size is set to True, then there are 1000 records in each batch. When set to False, then each batch is between 10 and 1000 rows.

</td>
</tr>
</table>



<a name="loio671cf97f398441d8bc83debae96efbea__section_pty_hm5_fnb"/>

## Input


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

inTable

</td>
<td valign="top">

Table

</td>
<td valign="top">

Table type port, which comes as output from other structured operators.

</td>
</tr>
</table>



<a name="loio671cf97f398441d8bc83debae96efbea__section_p31_rm5_fnb"/>

## Output


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

outMessage

</td>
<td valign="top">

Message

</td>
<td valign="top">

Outputs a message object with the following definition:

-   Body: The fully qualified name of the target table.
-   Attributes: producer.totalRows: Number of rows written to the target.
-   Encoding: string



</td>
</tr>
</table>



<a name="loio671cf97f398441d8bc83debae96efbea__section_x1k_jq5_fnb"/>

## BW Advanced Datastore Activation

When the SAP Application Producer finishes writing to the Advanced Datastore object, the data needs to be activated on the BW system before it can be used. This can be done on the BW system by creating a BW Process Chain. Configure the BW process chain to activate the data in the Datastore object referenced in the SAP Application Producer. After the Process Chain is configured, saved, and activated, use the BW Process Chain operator in a graph to invoke the process chain and activate the data via a pipeline graph.

To load the data to BW and then activate it via a Process Chain, create a graph that includes a pipeline operator that runs a graph that writes the data to the BW DataStore. Then chain that graph to a pipeline operator that runs the graph to call the Process Chain that activates the data.

