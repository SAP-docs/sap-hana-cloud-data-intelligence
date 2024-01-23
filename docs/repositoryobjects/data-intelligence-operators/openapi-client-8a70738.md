<!-- loio8a70738566e6466eb8d0f7d68be80247 -->

# OpenAPI Client

The OpenAPI client operator is a convenient client that is suitable for invoking services described in a OpenAPI document. However, its use is not limited to those services described in OpenAPI documentation, and it can be used to invoke arbitrary REST services.



This client is expected to be configured with some default parameters. Some of these properties can be customized per call when the corresponding headers of the input message are set accordingly.

In particular, parameters defined for the operation such as header, path, query, form, and file parameters can be set in the message headers using header names in form openapi.type\_params.name, where type indicates one of the parameter types and name identifies the parameter name, respectively.

In other words, headers openapi.header\_params.name, openapi.path\_params.name, openapi.query\_params.name, openapi.form\_params.name, and openapi.file\_params.name are used to represent the corresponding name parameter for the operation. Parameter values are interpreted as string for scalar values and set to the corresponding parameters of the request message except for file parameters. The value of a file parameter can be set either to the path to a file or to the content of a file.

For example, to assign file "/opt/pictures/dog12.png" or its content to file parameter "foto," header openapi.file\_params.foto can be set to "/opt/pictures/dog12.png". Alternatively, this header can be set to the base64 representation of the content of this file while setting another parameter openapi.file\_params.foto\#name to its name "dog12.png" to indicate that the value of this file parameter is the content and not the file path. Parameters values for vector values are represented as arrays. All parameters except for the header parameters support vector values \(for example, \["sunny", "day"\] for two values "sunny" and "day"\).

In addition to the above parameters, if header message.request\_id is set in the input message, this header will be included in the output message so that each response message can be correlated to its corresponding request message. Furthermore, the status code is set in openapi.status\_code in the response message.

**Recognized Message Headers**


<table>
<tr>
<th valign="top">

Header

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

message.request.id

</td>
<td valign="top">

The ID for correlating a request and its response messages.

</td>
</tr>
<tr>
<td valign="top">

openapi.header\_params.x

</td>
<td valign="top">

Header parameter x.

</td>
</tr>
<tr>
<td valign="top">

openapi.path\_params.x

</td>
<td valign="top">

Path parameter x.

</td>
</tr>
<tr>
<td valign="top">

openapi.query\_params.x

</td>
<td valign="top">

Query parameter x.

</td>
</tr>
<tr>
<td valign="top">

openapi.form\_params.x

</td>
<td valign="top">

Form parameter x.

</td>
</tr>
<tr>
<td valign="top">

openapi.file\_params.x

</td>
<td valign="top">

File parameter x, where its value may represent the path to the file or the base64 encoded content of the file.

</td>
</tr>
<tr>
<td valign="top">

openapi.file\_params.x\#name

</td>
<td valign="top">

File name parameter for file parameter x, if set, represents the file name and the value of its file parameter represents the base64 encoded content.

</td>
</tr>
<tr>
<td valign="top">

openapi.path\_pattern

</td>
<td valign="top">

Overrides the default pathPattern parameter configured at the .

</td>
</tr>
<tr>
<td valign="top">

openapi.method

</td>
<td valign="top">

Overrides the default method parameter configured at the operator.

</td>
</tr>
<tr>
<td valign="top">

openapi.produces

</td>
<td valign="top">

Overrides the default produces parameter \(for example, the accepted response content types\) configured at the operator.

</td>
</tr>
<tr>
<td valign="top">

openapi.consumes

</td>
<td valign="top">

Overrides the default consumes parameter \(for example, the request content type\) configured at the operator.

</td>
</tr>
<tr>
<td valign="top">

openapi.auth\_scheme

</td>
<td valign="top">

Overrides the default authScheme parameter configured at the operator.

</td>
</tr>
<tr>
<td valign="top">

openapi.user

</td>
<td valign="top">

Overrides the default user configured at the operator.

</td>
</tr>
<tr>
<td valign="top">

openapi.password

</td>
<td valign="top">

Overrides the default password configured at the operator.

</td>
</tr>
<tr>
<td valign="top">

openapi.api\_key\_name

</td>
<td valign="top">

Overrides the default apiKeyName configured at the operator.

</td>
</tr>
<tr>
<td valign="top">

openapi.api\_key\_value

</td>
<td valign="top">

Overrides the default apiKeyType configured at the operator.

</td>
</tr>
<tr>
<td valign="top">

openapi.status\_code

</td>
<td valign="top">

Status code given in the response message.

</td>
</tr>
</table>

Several authentication schemes are supported by the OpenAPI Client operator. These include basic, APIKey, and OAuth authentication schemes. When OAuth is chosen and its oauth2Flow is set to accessCode, the user must use the UI option of the OpenAPI client operator to authorize the client instance so that it can retrieve an access token. In this case, the correct redirection URL for this client instance must be registered at the authorization provider. The redirection URL has the service path /service/v1/runtime/internal/redirect.

You can use this operator as is, on its own, by manually configuring its parameters and using a custom operator that forwards appropriate input messages to this operator. If you have an OpenAPI file, you can generate such custom operator and a demo graph using the generateOpenAPIClient REST operation of the engine. Refer to the API document \(swagger.yaml\) available at the installed Modeler instance for details.

See [OpenAPI Server](openapi-server-1e23998.md) for the server-side operator.



<a name="loio8a70738566e6466eb8d0f7d68be80247__section_sq1_nf3_vdb"/>

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

Host

</td>
<td valign="top">

host

</td>
<td valign="top">

string

</td>
<td valign="top">

The service's host optionally including the port.

Default: localhost:8090

</td>
</tr>
<tr>
<td valign="top">

Schemes

</td>
<td valign="top">

schemes

</td>
<td valign="top">

string

</td>
<td valign="top">

The transport protocols.

Default: http

</td>
</tr>
<tr>
<td valign="top">

Base Path

</td>
<td valign="top">

basePath

</td>
<td valign="top">

string

</td>
<td valign="top">

The service's base path.

Default: /service

</td>
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

Mandatory. The object containing the connection parameters to an OpenAPI server.

Default: \{\}

</td>
</tr>
<tr>
<td valign="top">

Path Pattern

</td>
<td valign="top">

pathPattern

</td>
<td valign="top">

string

</td>
<td valign="top">

The path pattern with optional path variables. Overridden by header openapi.path\\\_pattern.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Method

</td>
<td valign="top">

method

</td>
<td valign="top">

string

</td>
<td valign="top">

The method name. Overridden by header openapi.method.

Default: "GET"

</td>
</tr>
<tr>
<td valign="top">

Produces

</td>
<td valign="top">

produces

</td>
<td valign="top">

string

</td>
<td valign="top">

A comma-separated list of media types that can be produced by the operation. Overridden by header openapi.produces.

Default: "application/json"

</td>
</tr>
<tr>
<td valign="top">

Consumes

</td>
<td valign="top">

consumes

</td>
<td valign="top">

string

</td>
<td valign="top">

A comma-separated list of media types that can be consumed by the operation. Overridden by header openapi.consumes.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Include Response Headers

</td>
<td valign="top">

includeResponseHeaders

</td>
<td valign="top">

string

</td>
<td valign="top">

A comma-separated list of \(case-sensitive\) response header names that should be included in the output message. Overridden by header openapi.include\\\_response\\\_headers. The response header\(s\) of the given header key will be sent to the output Message attribute `openapi.header.<key>`.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Response Header Output Format

</td>
<td valign="top">

responseHeadersFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

If set to `single value`, each response header key configured in `includeResponseHeaders` will be represented by the first received response header with the given key. If there are more headers with the same key, then they will be ignored. If set to `multiple values` and if there are multiple response headers with the same key \(usually for Set-Cookies\), they will be concatenated using a "," separator according to HTTP standard RFC2616.

Default: "single value"

</td>
</tr>
<tr>
<td valign="top">

Use CSRF Token

</td>
<td valign="top">

useCsrfToken

</td>
<td valign="top">

bool

</td>
<td valign="top">

If set to true, the client automatically retrieves a csrf-token at its first request and uses it in its subsequent requests.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Max Concurrency

</td>
<td valign="top">

maxConcurrency

</td>
<td valign="top">

integer

</td>
<td valign="top">

The maximum number of concurrent requests that are handled per operator instance. If the message order must be preserved, set this value to 1.

Default: 8

</td>
</tr>
<tr>
<td valign="top">

Timeout

</td>
<td valign="top">

timeout

</td>
<td valign="top">

int

</td>
<td valign="top">

The timeout value in milliseconds to wait for a response.

Default: 300000

</td>
</tr>
<tr>
<td valign="top">

OAuth2 Token Fetch with SAP Cloud Connector Proxy

</td>
<td valign="top">

oauth2TokenFetchUseProxy

</td>
<td valign="top">

bool

</td>
<td valign="top">

Controls whether the SAP Cloud Connector proxy should be used when fetching the OAuth2 token through the `OAuth2 Token Endpoint` URL configured in the connection. If the token endpoint is public or not masked through SAP Cloud Connector, the proxy should be disabled with this configuration. It will only have effect if the connection is configured to use both OAuth2 and SAP Cloud Connector \(enabled via the `Gateway` configuration\).

</td>
</tr>
<tr>
<td valign="top">

Enable Insecure OAuth2 Token Cache

</td>
<td valign="top">

connInsecureCheck

</td>
<td valign="top">

bool

</td>
<td valign="top">

If set to true and configured for an OAuth2 authentication flow, the OAuth2 token is stored in and used from the shared file system from System Management. It is not recommended as the storage is not secure and any administrator would have access to it. Requires additional field to be checked: **I understand that this will store the OAuth tokens on the shared filesystem where they can be accessed by administrators**.

</td>
</tr>
</table>



<a name="loio8a70738566e6466eb8d0f7d68be80247__section_knq_5f3_vdb"/>

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

Input message where parameters are set in the headers and the optional content in body.

</td>
</tr>
</table>



<a name="loio8a70738566e6466eb8d0f7d68be80247__section_swc_cg3_vdb"/>

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

Output message where parameters are set in the headers and the optional content in body.

</td>
</tr>
</table>

