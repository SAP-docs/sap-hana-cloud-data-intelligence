<!-- loio8da19b12f4744ebca050b95889767ad0 -->

# Send Email

Sends e-mails. It uses an SMTP protocol. Every time data comes through the input port, a new e-mail is built and sent.





<a name="loio8da19b12f4744ebca050b95889767ad0__section_yql_2rx_cfb"/>

## Configuration Parameters

**Configuration Parameters**


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

Delete Attachments After Sending

</td>
<td valign="top">

deleteAttachmentAfterSending

</td>
<td valign="top">

bool

</td>
<td valign="top">

A flag that controls whether the files attached to the e-mail should be deleted after sending or not.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Default From Value

</td>
<td valign="top">

defaultFrom

</td>
<td valign="top">

string

</td>
<td valign="top">

The value of `email.from`, which will be used when none is received through the incoming message. If not set, the value of user will be considered.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Default to Value

</td>
<td valign="top">

defaultTo

</td>
<td valign="top">

\[\]string

</td>
<td valign="top">

The value of `email.to`, which will be used when none is received through the incoming message.

Default: \[\]

</td>
</tr>
<tr>
<td valign="top">

Default Subject Value

</td>
<td valign="top">

defaultSubject

</td>
<td valign="top">

string

</td>
<td valign="top">

The value of `email.subject`, which will be used when none is received through the incoming message.

Default: ""

</td>
</tr>
</table>

**Connection Parameters**


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

Connection

</td>
<td valign="top">

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Holds information about connection information for the services.

</td>
</tr>
<tr>
<td valign="top">

Configuration Type

</td>
<td valign="top">

configurationType

</td>
<td valign="top">

string

</td>
<td valign="top">

Defines which type of connection information will be used.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Connection ID

</td>
<td valign="top">

connectionID

</td>
<td valign="top">

string

</td>
<td valign="top">

The ID of the connection information to retrieve from the Configuration Manager.

Default: ""

</td>
</tr>
</table>



<a name="loio8da19b12f4744ebca050b95889767ad0__section_uf3_v2f_5db"/>

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

message

</td>
<td valign="top">

A message whose attributes will be used to fill the e-mail information and whose body will be used as the e-mail body. In case there are multiple entries for a same header, they can be separated by a comma.

Message Attributes:

*email.to* \(type `[]string`\). Mandatory. The recipient of the e-mail.

*email.from* \(type `string`\). Mandatory. The sender of the e-mail.

*email.subject* \(type `string`\). Mandatory. The subject of the e-mail.

*email.cc* \(type `[]string`\). The CC \(carbon copy\) of the e-mail.

*email.attachments* \(type `[]string`\). The attachments of the e-mail. It expects the name of the files that should be attached. The operator will read those files and add as attachment.

</td>
</tr>
</table>



<a name="loio8da19b12f4744ebca050b95889767ad0__section_wt3_bff_5db"/>

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

A string containing a list of all the recipients that received the e-mail, separated by semicolon \(;\).

</td>
</tr>
</table>



<a name="loio8da19b12f4744ebca050b95889767ad0__section_sfm_dff_5db"/>

## Limitations

-   The following characters cannot appear in message header names: `<>${}`.



<a name="loio8da19b12f4744ebca050b95889767ad0__section_n4h_nff_5db"/>

## Basic Usage

> ### Example:  
> Suppose alice@example.com wants to send an e-mail to bob@example.com containing the message: "Hi Bob! How are you doing? Best, Alice", and with the subject being "Greetings". The message arriving at the operator should look like this:
> 
> ```
> {"email.from": "alice@example.com", "email.to": "bob@example.com", "email.subject": "Greetings"}Hi Bob! How are you doing? Best, Alice
> ```

If attachments were to be included, the attribute "email.attachments" should be used.



<a name="loio8da19b12f4744ebca050b95889767ad0__section_bj2_z42_bfb"/>

## Security

The Send Email operator can automatically detect if the SMTP server uses transport layer security \(TLS\).

