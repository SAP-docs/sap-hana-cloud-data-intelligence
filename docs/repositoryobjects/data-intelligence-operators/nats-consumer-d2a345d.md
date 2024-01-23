<!-- loiod2a345dd3d224071a1a95d5044d38fb1 -->

# NATS Consumer

The NATS Consumer operator consumes messages from NATS and forwards them to the output port.





<a name="loiod2a345dd3d224071a1a95d5044d38fb1__section_sq1_nf3_vdb"/>

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

NATS URL

</td>
<td valign="top">

natsUrls

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The NATS address.

Default: "nats://localhost:4222"

</td>
</tr>
<tr>
<td valign="top">

Queue

</td>
<td valign="top">

queue

</td>
<td valign="top">

string

</td>
<td valign="top">

The queue name to form the messages queue group. For more information, check the NATS documentation.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Subject

</td>
<td valign="top">

subject

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The subject name to subscribe to.

Default: "subject"

</td>
</tr>
<tr>
<td valign="top">

Number of Retry Attempts

</td>
<td valign="top">

numRetryAttempts

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of attempts to retry.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Retry Period \(ms\)

</td>
<td valign="top">

retryPeriodInMs

</td>
<td valign="top">

int

</td>
<td valign="top">

The time period for each retry in milliseconds.

Default: 0

</td>
</tr>
</table>



<a name="loiod2a345dd3d224071a1a95d5044d38fb1__section_knq_5f3_vdb"/>

## Input

None.



<a name="loiod2a345dd3d224071a1a95d5044d38fb1__section_swc_cg3_vdb"/>

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

`message` 

</td>
<td valign="top">

message

</td>
<td valign="top">

A message with the body containing the data \(as a blob\) and with the attributes containing the `nats.subject` and `nats.reply` fields.

</td>
</tr>
</table>

