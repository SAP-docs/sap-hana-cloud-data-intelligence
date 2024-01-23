<!-- loio35e476acf7bb46c0b46f31cf3ee1be6e -->

# DQMm Client

The DQMm Client operator is a convenient client for sending requests to the Data Quality Management, microservices for location data \(DQM microservices\). DQM microservices is a service hosted on SAP BTP. For more information on DQM microservices, view ***Data Quality Management, Microservices for Location Data*.** 



Data Quality Management microservices supports two types of authentication schemes. These include basic and OAuth authentication schemes.



<a name="loio35e476acf7bb46c0b46f31cf3ee1be6e__section_sq1_nf3_vdb"/>

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

host

</td>
<td valign="top">

string

</td>
<td valign="top">

The service's host optionally including the port.

</td>
</tr>
<tr>
<td valign="top">

includeResponseHeaders

</td>
<td valign="top">

string

</td>
<td valign="top">

A list of response header names that should be included in the output message. Overridden by header openapi.include\\\_response\\\_headers.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

authScheme

</td>
<td valign="top">

string

</td>
<td valign="top">

The security scheme. The possible values are "basic" and "oauth2". Overridden by header openapi.auth\\\_scheme.

Default: "oauth2"

</td>
</tr>
<tr>
<td valign="top">

user

</td>
<td valign="top">

string

</td>
<td valign="top">

The user name used by "basic" security scheme. Overridden by header openapi.user.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

password

</td>
<td valign="top">

string

</td>
<td valign="top">

The password used by "basic" security scheme. Overridden by header openapi.user.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

oauth2Flow

</td>
<td valign="top">

string

</td>
<td valign="top">

The flow used by "oauth2" security scheme. The only possible value is "application".

Default: "application"

</td>
</tr>
<tr>
<td valign="top">

oauth2TokenUrl

</td>
<td valign="top">

string

</td>
<td valign="top">

The token URL used by "oauth2" security scheme.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

oauth2ClientId

</td>
<td valign="top">

string

</td>
<td valign="top">

The client ID used by "oauth2" security scheme.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

oauth2ClientSecret

</td>
<td valign="top">

string

</td>
<td valign="top">

The client secret used by "oauth2" security scheme.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

oauth2AdditionalHeaders

</td>
<td valign="top">

string

</td>
<td valign="top">

Optional headers added in a token request, given as \\\{"header1": "value", ...\\\}.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

useCsrfToken

</td>
<td valign="top">

bool

</td>
<td valign="top">

If set to true, the client automatically retrieves a CSRF-token at its first request and uses it in its subsequent requests.

Default: false

</td>
</tr>
<tr>
<td valign="top">

tlsCertificate

</td>
<td valign="top">

string

</td>
<td valign="top">

The file path to the TLS certificate file.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

tlsKey

</td>
<td valign="top">

string

</td>
<td valign="top">

The file path to the TLS private key file.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

tlsCa

</td>
<td valign="top">

string

</td>
<td valign="top">

The file path to the TLS certificate authority file.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

tlsSkipVerify

</td>
<td valign="top">

bool

</td>
<td valign="top">

If set to true, the client does not verify the server's certificate chain nor the host name.

Default: false

</td>
</tr>
</table>



<a name="loio35e476acf7bb46c0b46f31cf3ee1be6e__section_knq_5f3_vdb"/>

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

Input message, where parameters are set in the headers and the optional content in body.

</td>
</tr>
</table>



<a name="loio35e476acf7bb46c0b46f31cf3ee1be6e__section_swc_cg3_vdb"/>

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

Output message, where parameters are set in the headers and the optional content in body.

</td>
</tr>
</table>

**Related Information**  


[Data Quality Management, Microservices for Location Data](https://help.sap.com/viewer/d95546360fea44988eb614718ff7e959/Cloud/en-US)

