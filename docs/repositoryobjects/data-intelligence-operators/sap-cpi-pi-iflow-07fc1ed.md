<!-- loio07fc1ed4f341429c9d7305799d1293f9 -->

# SAP CPI-PI iFlow

The SAP CPI-PI iFlow operator provides the possibility to trigger iFlows in an SAP CPI system. It calls the set CPI system sending the received input data as payload. The response is emitted via the outbound port. Currently, only HTTP Basic Authentication is supported.



<a name="loio07fc1ed4f341429c9d7305799d1293f9__section_sq1_nf3_vdb"/>

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

Connection

</td>
<td valign="top">

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. Connection parameters and credentials setting the CPI backend to communicate with.

</td>
</tr>
<tr>
<td valign="top">

Use Custom HTTP verb

</td>
<td valign="top">

customHttpVerbToggle

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Enables providing a custom HTTP verb instead of a standard one \(as defined in RFC `7231`\).

Default: `false`

</td>
</tr>
<tr>
<td valign="top">

HTTP verb

</td>
<td valign="top">

httpVerb

</td>
<td valign="top">

string

</td>
<td valign="top">

Select or enter the HTTP verb that should be used for making the request. Toggles between a text field and a list according to whether a custom HTTP verb should be used.

Default: `POST`

</td>
</tr>
<tr>
<td valign="top">

iFlow path

</td>
<td valign="top">

iFlowPath

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory: Points to the iFlow that shall be triggered. This is the portion of the URL following the slash after the hostname or domain \(`https://my.cpisystem.sap.com/`\). This information can be found in CPI's dashboard after deploying a given iFlow. Must not start with a slash \(`/`\).

</td>
</tr>
<tr>
<td valign="top">

CSRF Protection Enabled for iFlow

</td>
<td valign="top">

csrfProtectediFlow

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Needs to be enabled for iFlows with the very common CSRF protection activated.

Default: `true`

</td>
</tr>
<tr>
<td valign="top">

Content Type

</td>
<td valign="top">

contentType

</td>
<td valign="top">

string

</td>
<td valign="top">

The content type that will be stated in the outgoing request. Common values are `application/json`,`application/xml` or `text/xml`.

Default: `application/json`

</td>
</tr>
<tr>
<td valign="top">

Retry attempts

</td>
<td valign="top">

retryAttempts

</td>
<td valign="top">

integer

</td>
<td valign="top">

In case an HTTP\(S\) request to the CPI system fails, it will be retried `n` times. Only responses in the range of `5xx` status codes trigger a retry; `4xx` status codes will lead to an immediate failure \(for example, authentication issues\). Waiting time between requests will grow exponentially but is capped at 20 seconds.

Default: `1`

</td>
</tr>
<tr>
<td valign="top">

Verify TLS certificates

</td>
<td valign="top">

verifyTLSCerts

</td>
<td valign="top">

boolean

</td>
<td valign="top">

In case the CPI system uses a self-signed certificate, you may want to disable the certificate validation performed during the TLS handshake.

> ### Caution:  
> Use this with caution as the replying host's identity will no longer be ensured.

Default: `true`

</td>
</tr>
<tr>
<td valign="top">

Outgoing request timeout

</td>
<td valign="top">

requestTimeout

</td>
<td valign="top">

string

</td>
<td valign="top">

Defines the maximum amount of time a request outgoing to the set CPI system is allowed to take before being canceled \(this does not necessarily stop the triggered iFlow inside CPI\). Valid suffixes are `ms`, `s`, `m`, `h`. Setting this to `0s` results in no timeout. Independently, underlying software or hardware layers may enforce shorter timeouts.

Default: `60s`

</td>
</tr>
</table>



<a name="loio07fc1ed4f341429c9d7305799d1293f9__section_knq_5f3_vdb"/>

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

`input` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Receives DH message objects. By setting the attribute `cpi.iflowpath`, it is possible to dynamically override the set iFlow path. By setting attributes with the prefix `cpi.customheader`, it is possible to define custom headers \(and also override other headers like `content-type`\) in a programmatic way. For example, a header named SOAPAction could be set by adding an attribute `cpi.customheader.SOAPAction` to the message sent to the operator.

</td>
</tr>
</table>



<a name="loio07fc1ed4f341429c9d7305799d1293f9__section_swc_cg3_vdb"/>

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

`output` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Emits messages containing the response of the CPI system. In case an error occurred, the error message, if any, will be contained. The `message.error` attribute will be set accordingly.

</td>
</tr>
</table>

