<!-- loio6a7d923376924374ad16ff789a1c0943 -->

# Notification

The Notification operator helps send email notifications at certain points in the data workflow execution.



The message body contains technical information that the Notification operator receives at its input port from the previous operator in the data workflow.



<a name="loio6a7d923376924374ad16ff789a1c0943__section_ufc_dzc_l2b"/>

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

Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Connection ID that references a connection to an SMTP server.

</td>
</tr>
<tr>
<td valign="top">

Delete attachments after sending

</td>
<td valign="top">

boolean

</td>
<td valign="top">

A flag that controls whether the files attached to the email should be deleted after sending.

</td>
</tr>
<tr>
<td valign="top">

Default From Value

</td>
<td valign="top">

string

</td>
<td valign="top">

The value of `email.from`, which will be used when no value is received through the incoming message.

</td>
</tr>
<tr>
<td valign="top">

Default To Value

</td>
<td valign="top">

array

</td>
<td valign="top">

The value of `email.to`, which will be used when no value is received through the incoming message.

</td>
</tr>
<tr>
<td valign="top">

Default Subject Value

</td>
<td valign="top">

string

</td>
<td valign="top">

The value of `email.subject`, which will be used when no value is received through the incoming message.

</td>
</tr>
</table>



<a name="loio6a7d923376924374ad16ff789a1c0943__section_swc_cg3_vdb"/>

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

any.\*

</td>
<td valign="top">

Accepts a message whose attributes will be used to fill the email information and whose body will be used as the email body. If there are multiple entries for a same header, they can be separated by comma.

Message attributes:

-   email.to \(type string\) mandatory: The recipient of the email.

-   email.from \(type string\) mandatory: The sender of the email.

-   email.subject \(type string\) mandatory: The subject of the email.

-   email.cc \(type string\): The CC’s of the email.

-   email.attachments \(type string\): The attachments of the email.




</td>
</tr>
</table>



<a name="loio6a7d923376924374ad16ff789a1c0943__section_knq_5f3_vdb"/>

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

`out` 

</td>
<td valign="top">

string

</td>
<td valign="top">

String containing a list of all the recipients that received the email, separated by semicolon \(;\).

</td>
</tr>
</table>

