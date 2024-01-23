<!-- loiof1f6af01992145e288970f956aae5da9 -->

# Cloud Data Integration Consumer

The Cloud Data Integration Consumer operator \(com.sap.dh.cloud\_data\_integration\) is implemented in the subengine model and uses Flowagent for execution. To effectively read from it, it is necessary to connect this operator to a Flowagent-based producer operator \(for example, Flowagent File Producer\).



<a name="loiof1f6af01992145e288970f956aae5da9__section_jmy_q4l_m3b"/>

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

Source

</td>
<td valign="top">

string

</td>
<td valign="top">

JSON object containing the remote object reference, schema, and filters of the required entity set.

</td>
</tr>
<tr>
<td valign="top">

Page size

</td>
<td valign="top">

number

</td>
<td valign="top">

Number of records to be fetched within one page \(request\).

</td>
</tr>
<tr>
<td valign="top">

Polling period \(in minutes\)

</td>
<td valign="top">

number

</td>
<td valign="top">

The duration of polling new records in Delta mode.

</td>
</tr>
<tr>
<td valign="top">

Extraction mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Supports 2 modes of data extraction, Full and Delta.

</td>
</tr>
<tr>
<td valign="top">

Subscription ID

</td>
<td valign="top">

string

</td>
<td valign="top">

Unique external ID for creating subscriptions, required only in Delta mode.

</td>
</tr>
</table>



<a name="loiof1f6af01992145e288970f956aae5da9__section_u5k_1pl_m3b"/>

## Input

****


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

inDataSet

</td>
<td valign="top">

string

</td>
<td valign="top">

Optional input port for the dataset in case not configured via the UI.

</td>
</tr>
<tr>
<td valign="top">

inTrigger

</td>
<td valign="top">

any

</td>
<td valign="top">

Optional port for triggering the operator execution.

</td>
</tr>
</table>



<a name="loiof1f6af01992145e288970f956aae5da9__section_sp1_2pl_m3b"/>

## Output

****


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

outConfig

</td>
<td valign="top">

string.flowagent.config

</td>
<td valign="top">

Flowagent type port, which only Flowagent producers can consume \(for example, Flowagent File Producer\). To get the data as string, Flowagent CSV Producer can be used as producer.

</td>
</tr>
<tr>
<td valign="top">

outError

</td>
<td valign="top">

string

</td>
<td valign="top">

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

