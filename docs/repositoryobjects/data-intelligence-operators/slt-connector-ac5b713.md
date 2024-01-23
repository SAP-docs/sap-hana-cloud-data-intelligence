<!-- loioac5b7138c28a41fab51ccbbc8d2f574a -->

# SLT Connector

Use the SLT Connector operator to establish a connection between SAP Landscape Transformation Replication Server \(SLT\) and SAP Data Intelligence.



You can then use SLT to replicate tables from a source system into SAP Data Intelligence by creating a graph that includes SLT Connector for every table that you want to replicate.

Before you use this operator in a graph, you first need to create an SLT configuration in the ABAP-based system in which SLT is installed. To do so, run transaction code `LTRC` in the SLT system and specify the scenario type as *SAP Data Hub / SAP Data Intelligence*. For more information about replicating data to SAP Data Intelligence, see [https://help.sap.com/viewer/product/SAP\_LANDSCAPE\_TRANSFORMATION/2.0.14/en-US](https://help.sap.com/viewer/product/SAP_LANDSCAPE_TRANSFORMATION/2.0.14/en-US).

The part that you need later \(when using the operator\) is the mass transfer ID that is automatically assigned to your configuration: You have to specify it together with the table name and connection information.

When you then run the related graph, the table is automatically assigned to the mass transfer ID you defined previously. When the initial load is completed, when you choose transfer mode `Replication`, the system replicates the delta data of the source table and provides you with information about the original operation for each record \(I for Insert, D for Delete, U for Update\).

> ### Note:  
> When you stop a graph in the Modeler \(in SAP Data Intelligence\), SLT Connector suspends the replication process for the corresponding table in SLT.



<a name="loioac5b7138c28a41fab51ccbbc8d2f574a__section_szc_kpv_zkb"/>

## General Concepts

The following general concepts are relevant for this operator:

-   Authorizations

-   Versioning

-   Subscriptions


For a description of these concepts, see [ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md).



<a name="loioac5b7138c28a41fab51ccbbc8d2f574a__section_bwp_s5b_snb"/>

## New Features

As of V2, the output type for this operator has changed from `abap.*` to `message`, which also means that ABAP metadata is available. For more information, see below under *Output*.



<a name="loioac5b7138c28a41fab51ccbbc8d2f574a__section_sqr_jn2_djb"/>

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

Mandatory. The specific version of the operator to use.

Default: ""

</td>
<td valign="top">

V1, V2

</td>
</tr>
<tr>
<td valign="top">

Mass Transfer ID

</td>
<td valign="top">

Mass Transfer ID

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the mass transfer ID

Default: ""

</td>
<td valign="top">

V0, V1, V2

</td>
</tr>
<tr>
<td valign="top">

Table Name

</td>
<td valign="top">

Table Name

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the relevant table. Note: For logical tables that are part of a cluster table \(such as BSEG\), specify the name of the cluster table \(physical table\), for example RFBLG. Use the Cluster Table Splitter operator and link the output port of SLT Connector to the corresponding port of the Cluster Table Splitter. \(In the example, this would be bseg.\) If you do so, you only get the logical tables for which you specified ports. Otherwise, you get all logical tables that belong to the cluster table.

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

The ID of the subscription.

Default: ""

</td>
<td valign="top">

V1, V2

</td>
</tr>
<tr>
<td valign="top">

Chunk Size

</td>
<td valign="top">

Chunk size

</td>
<td valign="top">

string

</td>
<td valign="top">

See below for possible values

Default: ""

</td>
<td valign="top">

V0

</td>
</tr>
<tr>
<td valign="top">

Records per Roundtrip

</td>
<td valign="top">

chunkSize

</td>
<td valign="top">

integer

</td>
<td valign="top">

Maximum number of records to be output in one go \*\)

</td>
<td valign="top">

V1, V2

</td>
</tr>
<tr>
<td valign="top">

Transfer Mode

</td>
<td valign="top">

action

</td>
<td valign="top">

string

</td>
<td valign="top">

Can take the following values:

-   Initial Load - initial load only

-   Replication - replication of delta information \(including initial load\)
-   Delta Load - replication of delta information only \(no initial load\)

Default: "Initial Load"

</td>
<td valign="top">

V0, V1, V2

</td>
</tr>
</table>

\*\) The actual number of records per roundtrip depends on a variety of factors, but cannot be larger than the value you specify here. Possible values are all integer numbers from 1 to 500,000. Default: 50,000.

The Chunk Size parameter \(relevant for V0 only\) can take the following values:

-   1 record: Output the data record by record

-   1 portion: Output the source data in batches, one portion at a time. Depending on the transfer mode, it can take different values:

    -   Initial Load: The package size \(in bytes\) used for the initial load. By default, the package size is 8,000,000 bytes.

    -   Delta Load: The portion size is a number between 1 and 5,000 records.
    -   Replication: For the initial load, the portion size has the same meaning as specified above for initial load. For the replication itself, the portion size is a number between 1 and 5,000 records.




<a name="loioac5b7138c28a41fab51ccbbc8d2f574a__section_f5v_yjg_snb"/>

## Additional Information - Subscriptions and Related Topics

**Availability Information**

-   The subscription feature for this operator is available as of DMIS 2018 SP04, DMIS 2011 SP19, and SAP S/4HANA 2020 FPS00.

-   SAP S/4HANA 2020 FPS01:
    -   Resuming a dead graph is possible only if SLT Connector caught the error and forced the graph to die.

    -   If a graph containing the SLT Connector is stopped by means of the Stop button in the Modeler, the subscription is cleared automatically, and the table is stopped in the SLT system. If an error occurs and SLT Connector catches the error, the graph will be dead, and the subscription remains in the system. You can resume the graph by choosing subscription type *Existing* and the subscription ID for the subscription name you entered earlier, and you can remove the subscription as described below.

-   DMIS 2018 SP05 and DMIS 2011 SP20: If a graph is stopped after the initial load process has been completed successfully, the system automatically removes the subscription and removes the table in SLT. If, however, a running graph with transfer mode *Initial Load* is stopped before the data loading finishes, or if a running graph with transfer mode *Replication* or *Delta Load* is stopped, the subscription is not removed, and the table is suspended \(but not stopped\) in the SLT system. If you use the Cluster Table Splitter followed by SLT Connector, the subscription is **not** removed even after the data loading is finished.

-   V2 of the SLT Connector is available as of SAP Data Intelligence 3.0, but not with older on-premise releases of SAP Data Intelligence.

-   In combination with some DMIS releases, a minimum release of SAP Data Intelligence is required for the functionality to work. For details, see SAP Note [2892183](https://me.sap.com/notes/2892183)

**Function**

When you create a graph that includes the SLT Connector, you need to set the subscription type to *New* and enter a subscription name in the configuration panel.

> ### Example:  
> You want to replicate the table SFLIGHT for the first time. You have created a configuration in the SLT system. Its mass transfer ID \(MT ID\) is 001. You enter the following values in the SLT Connector configuration panel:
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
> 20200101SFLIGHT \(you can enter any name here\)
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Mass Transfer ID
> 
> </td>
> <td valign="top">
> 
> 001
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Table Name
> 
> </td>
> <td valign="top">
> 
> SFLIGHT
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Transfer Mode
> 
> </td>
> <td valign="top">
> 
> Replication
> 
> </td>
> </tr>
> </table>

To resume data loading for a graph after it was stopped, set the subscription type to *Existing* and choose the subscription ID that was generated automatically for your subscription name as well as the MT ID and the table name from the configuration panel.

You can find the subscription ID for your subscription name in either of the following ways:

-   Check the process logs of your executed pipeline in the Modeler

-   Look it up in the Resilience Subscription Eraser operator.
-   Find it in table DHAPE\_SUBSCR \(or LTAPE\_SUBSCR, respectively - depending on your ABAP system\) in the source ABAP-based system.

> ### Note:  
> -   As of DMIS 2018 SP05 and DMIS 2011 SP20, you use the Resilience Subscription Eraser operator to remove a subscription that you don't need anymore: Set the *Reader* object in the configuration panel to *Tables*, choose the subscription ID that you want to remove, and run the graph. The graph stops the table and removes the subscription from the SLT system.
> -   To load a table for which you removed a subscription earlier, set the subscription type to *New* to ensure that the table is loaded from scratch.
> -   As long as a graph has been stopped, but not yet removed, you cannot run another graph with subscription type *New* for the same table and MT ID.
> -   If you use the SLT Connector operator to integrate data from an ABAP source system, and your graph in SAP Data Intelligence terminates, you may get an error message like “Subscription <subscription\_name\> is being used by another graph” when you try to restart your failed graph. For more information about this error scenario, see SAP Note [3057246](https://me.sap.com/notes/3057246).



<a name="loioac5b7138c28a41fab51ccbbc8d2f574a__section_ghh_dhd_fjb"/>

## Input

-   None.




<a name="loioac5b7138c28a41fab51ccbbc8d2f574a__section_qqr_2hd_fjb"/>

## Output

-   For V0 and V1: outData: Output the CDS data; type: `abap.*`

-   As of V2: outMessageData: Output the CDS data; type: `message`


If you use V2 of the SLT Connector, the output operator provides a message output with metadata information in the header of the message including information about the column names with respective data types as well as the lastBatch attribute \(type boolean\) that indicates if the current batch is the last one.

Attributes:

-   Fields: object metadata from ABAP source system including field names and data types provided in json format

-   message.lastBatch \(type boolean\): boolean that indicates if the current batch is the last one in the data ingestion process

    Note: The lastBatch attribute is currently meant to be used in initial load scenarios only. If you run the graph in delta load or replication mode, the graph is expected to run permanently for capturing changes, and therefore the lastBatch attribute will never switch to 'true'.

-   message.batchIndex \(type integer\): number that indicates which batch is being processed, starting from 0.

