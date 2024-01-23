<!-- loioe7fd7dee19d54cc0a967d99f02d0f47f -->

# NATS Producer

The NATS Producer operator receives a message from the input port and publishes it into NATS.



<a name="loioe7fd7dee19d54cc0a967d99f02d0f47f__section_sq1_nf3_vdb"/>

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

Subject

</td>
<td valign="top">

subjects

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

numberRetryAttempts

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

The time period between each retry in milliseconds.

Default: 0

</td>
</tr>
</table>



<a name="loioe7fd7dee19d54cc0a967d99f02d0f47f__section_knq_5f3_vdb"/>

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

`message` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Message with the content to be published on its body. The body type should either be blob \(`\[\]byte`\) or string.

</td>
</tr>
</table>



<a name="loioe7fd7dee19d54cc0a967d99f02d0f47f__section_swc_cg3_vdb"/>

## Output

None.

