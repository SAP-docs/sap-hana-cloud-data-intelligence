<!-- loiodf331fcbeea244f887bb2ab90378e277 -->

# ABAP CDS Reader

Use the ABAP CDS Reader operator to read data from a CDS view.



You can specify which action the system should take:

-   Read all the data from the CDS view once \(initial load\)
-   Initial load and then follow up on subsequent changes \(replication\)
-   Follow up on changes only without doing an initial load first \(delta load\)



<a name="loiodf331fcbeea244f887bb2ab90378e277__section_szc_kpv_zkb"/>

## General Concepts

The following general concepts are relevant for this operator:

-   Authorizations

-   Versioning

-   Subscriptions


For a description of these concepts, see [ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md).



<a name="loiodf331fcbeea244f887bb2ab90378e277__section_bwp_s5b_snb"/>

## New Features

As of V2, the output type for this operator has changed from `abap.*` to `message`, which also means that ABAP metadata is available for CDS Reader. For more information, see below under *Output*



> ### Note:  
> When you do an initial load using V0 or V1 of the ABAP CDS Reader operator, it sends out an empty string when all the data has been transferred. The subsequent operator takes this empty string as the signal that the initial load is finished, and proceeds with the next actions \(for example, 'stop the graph'\). Since the output port type is `abap.*`, you can use the ABAP Converter operator to format the output data. For the empty string, the ABAP Convertor operator can format the empty string to the empty content. The CDS view with dataExtraction annotations must be enabled for the ABAP Converter operator according to the format value of the property format.
> 
> csv: ""
> 
> json: \{"DATA":""\}
> 
> xml: <?xml version=“1.0” encoding=“utf-16”?\> <asx:abap xmlns:asx=“http://www.sap.com/abapxml" version=“1.0” \> gt; gt; gt; gt;
> 
> The CDS view with dataExtraction annotations must be enabled for replication \(including initial load\) and replication \(delta load\) extraction. As of SAP S/4HANA 2020, you can use the CDS view I\_DataExtractionEnabledView to check if the actions replication \(including initial load\) and replication \(delta load\) are possible for a CDS view.



<a name="loiodf331fcbeea244f887bb2ab90378e277__section_sqr_jn2_djb"/>

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

Mandatory. The connection information for the remote ABAP system. You can select a predefined ABAP connection from the Connection Manager.

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

ABAP CDS Name

</td>
<td valign="top">

cdsname

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the CDS view. Note that depending on authorizations not all CDS views are available.

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

The name of the subscription

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

Transfer Mode

</td>
<td valign="top">

action

</td>
<td valign="top">

string

</td>
<td valign="top">

Can take one of the following values:

-   Initial Load -initial load only

-   Replication - replication of delta information \(including initial load\)

-   Delta Load - replication of delta information only \(no initial load\)

-   Default: "Initial Load"




</td>
<td valign="top">

V0, V1, V2

</td>
</tr>
<tr>
<td valign="top">

Records per Roundtrip

</td>
<td valign="top">

Chunk size

</td>
<td valign="top">

integer

</td>
<td valign="top">

Maximum number of records to be output in one go \*\)

</td>
<td valign="top">

V0, V1, V2

</td>
</tr>
</table>

\*\) The actual number of records per roundtrip depends on a varieyt of factors, but cannot be larger than the value you specify here. Possible values are all integer numbers from 1 to 1,000,000. Default: 50,000.



<a name="loiodf331fcbeea244f887bb2ab90378e277__section_wct_s1c_snb"/>

## Additional Information - Subscriptions and Related Topics

**Availability Information**

-   The subscription feature is available for this operator as of SAP S/4HANA 2020 FPS00.

-   The Resilience Subscription Eraser operator does not work for CDS Reader subscriptions in SAP S/4HANA OP 2020 FPS00. For more information, see [2967162](https://me.sap.com/notes/2967162).
-   V2 of the ABAP CDS Reader is available as of SAP Data Intelligence 3.0, but not with older on-premise releases of SAP Data Intelligence.


**Function**

When you create a graph that includes the ABAP CDS Reader, you need to set the subscription type to *New* and enter a subscription name in the configuration panel.

> ### Example:  
> You want to replicate a CDS view called EXAMPLECDSV for the first time. You enter the following values in the configuration panel:
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
> 20200101EXAMPLECDSV \(you can enter any name here\)
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> ABAP CDS Name
> 
> </td>
> <td valign="top">
> 
> EXAMPLECDSV
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

To resume data loading for a graph after it was stopped, set the subscription type to *Existing* and choose the subscription ID that was generated automatically for your subscription name as well as the CDS name and the transfer mode from the configuration panel.

You can find the subscription ID for your subscription name in either of the following ways:

-   Check the process logs of your executed pipeline in the Modeler

-   Look it up in the Resilience Subscription Eraser operator.
-   Find it in table DHAPE\_SUBSCR \(or LTAPE\_SUBSCR, respectively - depending on your ABAP system\) in the source ABAP-based system.

> ### Note:  
> -   If the transfer mode is *Initial Load* and the initial load process was completed successfully, the subscription is removed automatically.
> 
> -   If the transfer mode is *Initial Load* and the graph is stopped before the initial load finishes, or if the transfer mode is *Replication* or *Delta Load*, the data loading is stopped when the graph is stopped, but the subscription is **not** removed.
> -   *CDS View* and select the subscription ID that you want to use. For more information about how to proceed, see [ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md).



<a name="loiodf331fcbeea244f887bb2ab90378e277__section_ghh_dhd_fjb"/>

## Input

-   None.




<a name="loiodf331fcbeea244f887bb2ab90378e277__section_qqr_2hd_fjb"/>

## Output

-   For V0 and V1: outData: Output the CDS data; type: `abap.*`

-   As of V2: outMessageData: Output the CDS data; type: `message`


In addition, the output data type depends on the type of the CDS view that is being read. It is extended by an additional field that specifies the operation \(“I” for Insert, “U” for Upsert and “D” for Delete\).

If you use V2 of the CDS Reader, the output operator provides a message output with metadata information in the header of the message including information about the column names with respective data types as well as the lastBatch attribute \(type boolean\) that indicates if the current batch is the last one.

Attributes:

-   Fields: object metadata from ABAP source system including field names and data types provided in json format

-   message.lastBatch \(type boolean\): boolean that indicates if the current batch is the last one in the data ingestion process

    Note: The lastBatch attribute is currently meant to be used in initial load scenarios only. If you run the graph in delta load or replication mode, the graph is expected to run permanently for capturing changes, and therefore the lastBatch attribute will never switch to 'true'.

-   message.batchIndex \(type integer\): number that indicates which batch is being processed, starting from 0.

