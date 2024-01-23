<!-- loio4f7400ea42b444ee827fa0e55c7f5bf7 -->

# Data Services Transform

Use the Data Services Transform operator to perform data transformations, such as projection, filter, and column operations and to move data from an on-premise source to SAP Data Intelligence.



This operator can output to any operator that provides vType support. This operator runs the data flow in the remote SAP Data Services system.

This operator has two tabs: *Configuration* and *Graphical Editor*. The remote job runtime environment is configured under *Configuration* followed by data flow modeleing under *Graphical Editor*.



<a name="loio4f7400ea42b444ee827fa0e55c7f5bf7__section_sq1_nf3_vdb"/>

## Configuration Parameters

**Configuration Tab**


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

Connection ID

</td>
<td valign="top">

string

</td>
<td valign="top">

Connection to remote SAP Data Services system.

</td>
</tr>
<tr>
<td valign="top">

Repository

</td>
<td valign="top">

string

</td>
<td valign="top">

Remote SAP Data Services system repository name.

</td>
</tr>
<tr>
<td valign="top">

Job Server

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

Substitution Parameters

</td>
<td valign="top">

string

</td>
<td valign="top">

Substitution parameters used for data flow.

</td>
</tr>
</table>

**Graphical Editor Tab**


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Data Source

</td>
<td valign="top">

Remote datastore table used for the source of the data flow. Status of the remote datastore can be checked from here.

Supported datastores: Oracle, Microsoft SQL server.

</td>
</tr>
<tr>
<td valign="top">

Transformation

</td>
<td valign="top">

Add or remove columns, filter and column functions for the data flow.

</td>
</tr>
</table>



<a name="loio4f7400ea42b444ee827fa0e55c7f5bf7__section_vcs_zzm_4qb"/>

## Additional Information

-   This operator requires remote SAP Data Services system version to be 4.2 SP14 Patch 16 or higher.
-   Any unconnected output port results in a graph failure.
-   Only one Data Services Transform operator per graph is allowed.
-   This operator does not work if it is connected to another Data Services Transform operator.
-   The user interface allows you to add more than one Data Services Transform operator, but it is not a supported configuration due to potential resource issues.

