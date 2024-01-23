<!-- loio6040d594a83c4b75a4649302e61cd6ab -->

# SAP CP EM Producer

Publishes messages from SAP Data Intelligence to a topic in SAP BTP Enterprise Messaging.



<a name="loio6040d594a83c4b75a4649302e61cd6ab__section_jmy_q4l_m3b"/>

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

CP EM Connection

</td>
<td valign="top">

emConnection

</td>
<td valign="top">



</td>
<td valign="top">

Connection to an SAP BTP enterprise messaging service.

Default: none

</td>
</tr>
<tr>
<td valign="top">

Target Topic

</td>
<td valign="top">

target

</td>
<td valign="top">

string

</td>
<td valign="top">

SAP BTP enterprise messaging topic to which messages are written. It must conform to the namespace of the Message Client; otherwise, an error message is sent to the `error` outport.

The topic name must start with the Message Client's namespace followed by a slash \(\`/\`\) and one or more alphanumerical components separated by a slash \(\`/\`\). Each component may contain capital or lowercase letters \(\`A−Z\`, \`a−z\`\), digits \(\`0−9\`\), and hyphens \(\`-\`\). The topic name \(including namespace\) must not be longer than 150 characters.

Default: none

</td>
</tr>
<tr>
<td valign="top">

No. of Reconnect Tries

</td>
<td valign="top">

reconnTries

</td>
<td valign="top">

integer

</td>
<td valign="top">

Number of attempts to reconnect the SAP CP EM Consumer to the SAP BTP enterprise messaging service after it has been disconnected \(either due to an error or by the server; in the former case the error is provided at the *error* output port\).

Default: `0`

</td>
</tr>
<tr>
<td valign="top">

Reconnect Wait Time

</td>
<td valign="top">

reconnWait

</td>
<td valign="top">

integer

</td>
<td valign="top">

Time in ms to wait between two consecutive reconnection attempts.

Default: `0`

</td>
</tr>
<tr>
<td valign="top">

Max. no. of Messages

</td>
<td valign="top">

maxCount

</td>
<td valign="top">

integer

</td>
<td valign="top">

Number of messages that is read from the SAP BTP enterprise messaging service before disconnecting the consumer. If set to `0`, the consumer is not automatically disconnected from the SAP BTP enterprise messaging service.

Default: `0`

</td>
</tr>
<tr>
<td valign="top">

Log after Messages

</td>
<td valign="top">

logCount

</td>
<td valign="top">

integer

</td>
<td valign="top">

Number of received messages after which a log entry \(stating the message count\) is written. If set to `0`, no message counts are logged.

Default: `0`

</td>
</tr>
</table>



<a name="loio6040d594a83c4b75a4649302e61cd6ab__section_u5k_1pl_m3b"/>

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

payload

</td>
<td valign="top">

message

</td>
<td valign="top">

A message containing the payload data to be published via SAP BTP enterprise messaging.

</td>
</tr>
</table>



<a name="loio6040d594a83c4b75a4649302e61cd6ab__section_sp1_2pl_m3b"/>

## Output


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

ack

</td>
<td valign="top">

number

</td>
<td valign="top">

The number of messages that have successfully been sent to the SAP BTP enterprise messaging service by the SAP CP EM Producer. This output is generated after each successfully published message.

</td>
</tr>
<tr>
<td valign="top">

done

</td>
<td valign="top">

string

</td>
<td valign="top">

Indicates that the given *Max. no. of Messages* have been received by outputting `true`. This port never outputs anything if the *Max. no. of Messages* parameter is not set or set to `0`.

</td>
</tr>
<tr>
<td valign="top">

error

</td>
<td valign="top">

message.error

</td>
<td valign="top">

A message containing an error.

</td>
</tr>
</table>

