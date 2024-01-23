<!-- loioa81089c64c9044d6888bf6395a6cbf6e -->

# SAP CP EM Consumer

Receives messages from a queue in SAP BTP Enterprise Messaging and provides them for consumption in SAP Data Intelligence.



<a name="loioa81089c64c9044d6888bf6395a6cbf6e__section_jmy_q4l_m3b"/>

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

Source Queue

</td>
<td valign="top">

source

</td>
<td valign="top">

string

</td>
<td valign="top">

SAP BTP enterprise messaging queue from which messages are read. The queue must exist on the SAP BTP enterprise messaging service instance. If the queue does not exist, an error message is sent to the `error` outport.

The queue name must start with the Message Client's namespace followed by a slash \(\`/\`\) and one or more alphanumerical components separated by a slash \(\`/\`\). Each component may contain capital or lowercase letters \(\`A−Z\`, \`a−z\`\), digits \(\`0−9\`\), underscores \(\`\_\`\), hyphens \(\`-\`\), and dots \(\`.\`\). The queue name \(including namespace\) must not be longer than 164 characters.

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



<a name="loioa81089c64c9044d6888bf6395a6cbf6e__section_u5k_1pl_m3b"/>

## Input

None.



<a name="loioa81089c64c9044d6888bf6395a6cbf6e__section_sp1_2pl_m3b"/>

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

payload

</td>
<td valign="top">

message

</td>
<td valign="top">

A message containing the payload data received from SAP BTP enterprise messaging.

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

