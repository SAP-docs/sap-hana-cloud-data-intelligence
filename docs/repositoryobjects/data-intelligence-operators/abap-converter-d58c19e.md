<!-- loiod58c19e5330f4975a2b644bc17ac0ce9 -->

# ABAP Converter

Use the ABAP Converter operator to convert a generic ABAP data type to string using the CSV, JSON, or XML format.



Note: As of SAP Data Intelligence Cloud 2107, the old ABAP Converter has been deprecated and replaced with a new operator, which is also called ABAP Converter. The new one has ' ' \(instead of CSV\) as the default output format and includes some technical prerequisites for dynamically supporting more configurations in the future.



<a name="loiod58c19e5330f4975a2b644bc17ac0ce9__section_szc_kpv_zkb"/>

## General Concepts

The following general concepts are relevant for this operator:

-   Authorizations


For a description of these concepts, see [ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md).



<a name="loiod58c19e5330f4975a2b644bc17ac0ce9__section_osv_rbv_zkb"/>

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

Default: " "

</td>
</tr>
<tr>
<td valign="top">

Format

</td>
<td valign="top">

format

</td>
<td valign="top">

string

</td>
<td valign="top">

The output format. Supported formats are CSV, JSON, and XML.

Default: " "

</td>
</tr>
</table>



<a name="loiod58c19e5330f4975a2b644bc17ac0ce9__section_u35_33c_xdb"/>

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

in

</td>
<td valign="top">

abap.\*

</td>
<td valign="top">

Contents to be converted.

</td>
</tr>
</table>



<a name="loiod58c19e5330f4975a2b644bc17ac0ce9__section_jxw_y3c_xdb"/>

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

out

</td>
<td valign="top">

string

</td>
<td valign="top">

Contents that were converted.

</td>
</tr>
</table>

