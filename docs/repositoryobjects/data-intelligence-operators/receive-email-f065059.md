<!-- loiof065059ee27e42e78391f1e687504c28 -->

# Receive Email

Receives emails. The protocol used is IMAP Version 4rev1. The operator fetches emails automatically if the in port is not connected. When the port is connected, the operator fetches emails whenever a new entry arrives. The output is received as single messages, each related to a single email.



<a name="loiof065059ee27e42e78391f1e687504c28__section_yql_2rx_cfb"/>

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

Maximum Entries

</td>
<td valign="top">

Maximum entries

</td>
<td valign="top">

integer

</td>
<td valign="top">

The maximum number of entries the system will fetch. If `maxEntries` is higher than the mailbox amount of emails, it will send only the emails contained in the mailbox. If `maxEntries` is smaller than the mailbox occupancy, it will send only the '`maxEntries`' newest items.

This property is also considered when input port is not connected.

Default: 10

</td>
</tr>
<tr>
<td valign="top">

Mailbox

</td>
<td valign="top">

Mailbox

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory: The mailbox from which emails will be retrieved. This will be used only when in Polling mode.

Default: "inbox"

</td>
</tr>
<tr>
<td valign="top">

Poll Period

</td>
<td valign="top">

Poll period

</td>
<td valign="top">

integer

</td>
<td valign="top">

The poll period \(in Milliseconds\). Meaning that every 'pollPeriod' seconds, a new email fetch will be done. This will be used only when in Polling mode.

Default: 1000

</td>
</tr>
<tr>
<td valign="top">

Only Output Unread Emails

</td>
<td valign="top">

Only output unread emails

</td>
<td valign="top">

boolean

</td>
<td valign="top">

When set to true, the system will output only emails that have not been previously read.

Default: true

</td>
</tr>
</table>

> ### Note:  
> Use `Connection Management` for defining connections over the manual option.

**Connection Parameters**


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

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Information about connection details for the services.

</td>
</tr>
<tr>
<td valign="top">

configurationType

</td>
<td valign="top">

string

</td>
<td valign="top">

Which type of connection information will be used.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

connectionID

</td>
<td valign="top">

string

</td>
<td valign="top">

The ID of the connection information to retrieve from the Connection Management Service.

Default: ""

</td>
</tr>
</table>



<a name="loiof065059ee27e42e78391f1e687504c28__section_svv_nw2_5db"/>

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

string

</td>
<td valign="top">

This port will inform what mailbox should be fetched. When this port is used, it disables the Polling mode and performs an email fetch for every single entry arriving at this port.

</td>
</tr>
</table>



<a name="loiof065059ee27e42e78391f1e687504c28__section_cy5_qw2_5db"/>

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

message

</td>
<td valign="top">

A message containing the Message Attributes and the Body of an email. The email body can be either in plain-text format or HTML format.

Message Attributes:

*email.to* \(type Address\). The recipient of the email.

*email.from* \(type Address\). The sender of the email.

*email.subject* \(type string\). The subject of the email.

*email.cc* \(type Adress\). The carbon copy recipients of the email.

*email.date* \(type time.Time\). The date when the email was received at the server.

</td>
</tr>
</table>



<a name="loiof065059ee27e42e78391f1e687504c28__section_t12_xnf_5db"/>

## Additional Object Information


<dl>
<dt><b>

Address

</b></dt>
<dd>

An object that has two fields, Name\(type string\) and Address\(type string\). The Name field is used to describe the name of the person \(or entity\) who sent the email, which may be empty. The Address field contains the email which the email was received from, this is always filled.



</dd>
</dl>

