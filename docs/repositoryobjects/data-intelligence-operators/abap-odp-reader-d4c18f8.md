<!-- loiod4c18f8032b042b3a1c56983d048622d -->

# ABAP ODP Reader

Use this operator to read data from an object for operational data processing \(ODP object\).



The following extraction modes are supported:

-   FULL - one-time load of the entire ODP object:

    As soon as it has output all data from the ODP queue, the ABAP ODP Reader \(V0 and V1\) sends an empty string to the subsequent operator to let it know that it can start. \(As of V2, this is no longer necessary as the corresponding information is included in the metadata.\)

-   DELTA - Replication of delta information \(including initial load\)


As of DMIS 2011 SP19 and DMIS 2018 SP04, the ABAP ODP Reader supports projection and filtering if used together with the Data Transfer operator.



<a name="loiod4c18f8032b042b3a1c56983d048622d__section_szc_kpv_zkb"/>

## General Concepts

The following general concepts are relevant for this operator:

-   Authorizations

-   Versioning

-   Subscriptions


For a description of these concepts, see [ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md).



<a name="loiod4c18f8032b042b3a1c56983d048622d__section_bwp_s5b_snb"/>

## New Features

As of V2, the output type for this operator has changed from `abap.*` to `message`, which also means that ABAP metadata is available. For more information, see below under *Output*.



<a name="loiod4c18f8032b042b3a1c56983d048622d__section_vxr_rhd_fjb"/>

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
<th valign="top">

Relevant in Version

</th>
</tr>
<tr>
<td valign="top">

ABAP Connection

</td>
<td valign="top">

connectionID

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The connection information for the ABAP-based remote system. You can select a predefined ABAP connection from the Connection Manager.

Default: ""

</td>
<td valign="top">

V0, V1, V2

</td>
</tr>
<tr>
<td valign="top">

Version

</td>
<td valign="top">

operatorID

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The specific version of the operator.

Default: ""

</td>
<td valign="top">

V1, V2

</td>
</tr>
<tr>
<td valign="top">

Context

</td>
<td valign="top">

context

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the ODP context. Can take one of the following values:

-   ODP\_BW

-   ODP\_SAPI

Default: ""

</td>
<td valign="top">

V0, V1, V2

</td>
</tr>
<tr>
<td valign="top">

ODP Object Name

</td>
<td valign="top">

odpname

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the ODP object - only used if the ODP oject is not specified in the adapted dataset.

Default: ""

</td>
<td valign="top">

V0, V1, V2

</td>
</tr>
<tr>
<td valign="top">

Extraction Mode

</td>
<td valign="top">

extractionMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Can take one of the following values:

-   FULL

-   DELTA



</td>
<td valign="top">

V0, V1, V2

</td>
</tr>
<tr>
<td valign="top">

Polling Period

</td>
<td valign="top">

pollingPeriod

</td>
<td valign="top">

string

</td>
<td valign="top">

Only relevant for DELTA. The polling period specifies the amount of time in seconds until the operator will make the next attempt to fetch data after an attempt that did not return any data.

Default: ""

</td>
<td valign="top">

V0, V1, V2

</td>
</tr>
<tr>
<td valign="top">

Subscription Type

</td>
<td valign="top">

subscriptionType

</td>
<td valign="top">

string

</td>
<td valign="top">

Can take one of the following values:

-   New - new subscription

-   Existing - reuse existing subscription

Default: "New"

</td>
<td valign="top">

V1, V2

</td>
</tr>
<tr>
<td valign="top">

Subscription Name

</td>
<td valign="top">

subscriptionName

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the subscription.

Default: ""

</td>
<td valign="top">

V1, V2

</td>
</tr>
<tr>
<td valign="top">

Subscription ID

</td>
<td valign="top">

subscriptionID

</td>
<td valign="top">

string

</td>
<td valign="top">

The unique identifier of the subscription.

Default: ""

</td>
<td valign="top">

V1, V2

</td>
</tr>
</table>



<a name="loiod4c18f8032b042b3a1c56983d048622d__section_irc_42h_snb"/>

## Additional Information - Subscriptions and Related Topics

**Availability Information**

-   The subscription feature is available for this operator as of DMIS 2018 SP04 and DMIS 2011 SP19.

-   V2 of the SLT Connector is available as of SAP Data Intelligence 3.0, but not with older on-premise releases of SAP Data Intelligence.


**Function**

When you create a graph that includes the ABAP ODP Reader, you need to set the subscription type to `New` and enter a subscription name in the configuration panel.

> ### Example:  
> You want to do a delta load for an object called EXAMPLEODP under context ODP\_SAPI for the first time. You enter the following values in the ODP Reader configuration panel:
> 
> 
> <table>
> <tr>
> <td valign="top">
> 
> Subscription Type
> 
> </td>
> <td valign="top">
> 
> New
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Subscription Name
> 
> </td>
> <td valign="top">
> 
> 20200101EXAMPLEODP \(you can enter any name here\)
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Context
> 
> </td>
> <td valign="top">
> 
> ODP\_SAPI
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> ODP Object Name
> 
> </td>
> <td valign="top">
> 
> EXAMPLEODP
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Extraction Mode
> 
> </td>
> <td valign="top">
> 
> DELTA
> 
> </td>
> </tr>
> </table>
> 
> To resume data loading for a graph after it was stopped, set the subscription type to `Existing` and choose the corresponding subscription ID for your subscription name, ODP context, and ODP name from the configuration panel.

> ### Note:  
> -   If the extraction mode is `FULL` and the load process was completed successfully, the subscription is removed automatically.
> 
> -   If the extraction mode is `FULL` and the graph is stopped before the load process finishes, or if the extraction mode is `DELTA`, the data loading is stopped when the graph is stopped, but the subscription is **not** removed.
> -   To remove a subscription that you don't need anymore, you use the Resilience Subscription Eraser operator: Set the Reader object in the configuration panel to *ODP Objects* and choose the subscription ID that you want to remove.



<a name="loiod4c18f8032b042b3a1c56983d048622d__section_ghh_dhd_fjb"/>

## Input

-   None.




<a name="loiod4c18f8032b042b3a1c56983d048622d__section_qqr_2hd_fjb"/>

## Output

-   For V0: outRecord: output the data record by record; type: abap.\*

-   For V0: outTable: output the data in batches; note that the default batch size is 10 MB an cannot be changed. Type: abap.\*

-   For V1: outData: Output the ODP data in batches of a fixed size of 10 MB each; type: `abap.*`

-   As of V2: outMessageData: Output the ODP data in batches of a fixed size of 10 MB each; type: `message`


If you use V2 of the ABAP ODP Reader, the output operator provides a message output with metadata information in the header of the message including information about the column names with respective data types as well as the lastBatch attribute \(type boolean\) that indicates if the current batch is the last one.

Attributes:

-   Fields: object metadata from ABAP source system including field names and data types provided in json format

-   message.lastBatch \(type boolean\): boolean that indicates if the current batch is the last one in the data ingestion process

    Note: The lastBatch attribute is currently meant to be used in initial load scenarios only. If you run the graph in delta load or replication mode, the graph is expected to run permanently for capturing changes, and therefore the lastBatch attribute will never switch to 'true'.

-   message.batchIndex \(type integer\): number that indicates which batch is being processed, starting from 0.

