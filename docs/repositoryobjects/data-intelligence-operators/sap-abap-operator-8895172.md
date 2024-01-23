<!-- loio88951726488745fbab4e2c800f367736 -->

# SAP ABAP Operator

Use the SAP ABAP Operator to make a standard operator implementation from your ABAP-based remote system available in SAP Data Intelligence. The SAP ABAP Operator dynamically adapts to the selected operator in the remote system.



> ### Note:  
> Only operators that were created in the SAP namespace in the remote ABAP-based system are displayed for selection with the SAP ABAP operator.



<a name="loio88951726488745fbab4e2c800f367736__section_yph_fhd_fjb"/>

## Procedure

1.  Add the SAP ABAP Operator to a graph.
2.  Open the *Configuration Panel*:
    1.  Select a predefined connection for the ABAP-based remote system.
    2.  Select an operator implementation from the ABAP-based remote system. The UI will adapt the SAP ABAP Operator to the selected operator implementation.
    3.  If required, enter the additional configuration values.

3.  Connect the operator to other operators as usual.



<a name="loio88951726488745fbab4e2c800f367736__section_szc_kpv_zkb"/>

## General Concepts

The following general concepts are relevant for this operator:

-   Authorizations


For a description of these concepts, see [ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md).



<a name="loio88951726488745fbab4e2c800f367736__section_my5_zgw_zkb"/>

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



<a name="loio88951726488745fbab4e2c800f367736__section_ghh_dhd_fjb"/>

## Input

-   None.




<a name="loio88951726488745fbab4e2c800f367736__section_qqr_2hd_fjb"/>

## Output

-   None.


