<!-- loiobd79a318d07b4dceb57f1f1a847aab93 -->

# Custom ABAP Operator

You can create your own custom operators in your ABAP-based remote system. To make these operators available in SAP Data Intelligence, use the Custom ABAP Operator. The Custom ABAP Operator adapts dynamically to the custom operator that you select in the remote system.



For more information about how to integrate ABAP function modules with SAP Data Intelligence using the Custom ABAP Operator, see [Integrating ABAP Function modules with SAP Data Intelligence in the SAP Community](https://blogs.sap.com/2021/06/01/integrating-abap-function-modules-with-sap-data-intelligence/).

> ### Note:  
> Only operators that were **not** created in the SAP namespace in the remote ABAP-based system are displayed for selection with the Custom ABAP Operator.



<a name="loiobd79a318d07b4dceb57f1f1a847aab93__section_yph_fhd_fjb"/>

## Procedure

1.  Add the Custom ABAP operator to a graph.
2.  Open the *Configuration Panel*:
    1.  Select a predefined connection for the remote ABAP system.
    2.  Select an operator implementation from the remote ABAP system. The user interface will adapt the Custom ABAP operator to the selected operator implementation.
    3.  If required, enter the additional configuration values.

3.  Connect the operator to other operators as usual.

For more details about how to create a custom ABAP operator, see the [User Guide for ABAP Integration in SAP Data Intelligence](https://help.sap.com/viewer/1c4ff4486dd04e47b32fe406111bfee8/3.0.latest/en-US/761715f7f2524b52a4e6c0708160dc5d.html).



<a name="loiobd79a318d07b4dceb57f1f1a847aab93__section_szc_kpv_zkb"/>

## General Concepts

The following general concepts are relevant for this operator:

-   Authorizations


For a description of these concepts, see [ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md).



## Configuration Parameters

****


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
</tr>
<tr>
<td valign="top">

ABAP Operator

</td>
<td valign="top">

operator

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. A predefined operator implementation from the remote ABAP system.

Default: ""

</td>
</tr>
</table>



<a name="loiobd79a318d07b4dceb57f1f1a847aab93__section_ghh_dhd_fjb"/>

## Input

-   None.




<a name="loiobd79a318d07b4dceb57f1f1a847aab93__section_qqr_2hd_fjb"/>

## Output

-   None.


