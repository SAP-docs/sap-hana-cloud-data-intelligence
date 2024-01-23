<!-- loiof6479feedf6740faa96f354a457f7b6e -->

# WAMP Producer

The WAMP Producer operator writes files to Web Application Messaging Protocol \(WAMP\).



<a name="loiof6479feedf6740faa96f354a457f7b6e__section_sq1_nf3_vdb"/>

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

wampServer

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The WAMP address.

Default: "ws://localhost:8000/ws"

</td>
</tr>
<tr>
<td valign="top">

realm

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The routing namespace and administrative domain.

Default: "turnpike.chat.realm"

</td>
</tr>
<tr>
<td valign="top">

topic

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The category name to which records are published.

Default: "testwamp"

</td>
</tr>
<tr>
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

retryPeriodInMs

</td>
<td valign="top">

int

</td>
<td valign="top">

The time period in milliseconds for each retry.

Default: 0

</td>
</tr>
</table>



<a name="loiof6479feedf6740faa96f354a457f7b6e__section_knq_5f3_vdb"/>

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

`inmessage` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The stream of records to publish.

</td>
</tr>
</table>



<a name="loiof6479feedf6740faa96f354a457f7b6e__section_swc_cg3_vdb"/>

## Output

None

