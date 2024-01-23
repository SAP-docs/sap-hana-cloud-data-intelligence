<!-- loiof6619b1123794a4fb47fe904859391a2 -->

# HTTP Client

The HTTP Client operator performs HTTP requests.



> ### Note:  
> The `OAuth2` and `ApiKey` authentication typea are not supported.



<a name="loiof6619b1123794a4fb47fe904859391a2__section_xsf_s3w_wlb"/>

## Operations

The client is capable of three main operations:

-   **Poll**: if *Polling Enabled* is set to "True", the operator sends GET requests to the server specified in *Poll Connection*. You can control the interval between requests with the *Polling Period* property.

-   **Post**: data received on the `in` port is sent as POST requests to the server specified in *Post Connection*.

-   **Custom requests**: each message received on the `inRequest` port specifies one request to be made.


The response to any of these operations is sent to the `outResponse` port, regardless of its status code. If this port is not connected, a status code outside the 2×× range raises an error. When the status code is in this range, the body of the response is also sent to the `out` port, if connected.



<a name="loiof6619b1123794a4fb47fe904859391a2__section_sq1_nf3_vdb"/>

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

Poll Enabled

</td>
<td valign="top">

pollingEnabled

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Determines whether the poll operation is enabled.

</td>
</tr>
<tr>
<td valign="top">

Poll Connection

</td>
<td valign="top">

getConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Holds the connection information for the poll operation. It is only used when *Polling Enabled* is "True". If a gateway is associated to this connection, it takes precedence over the *Proxy* setting.

</td>
</tr>
<tr>
<td valign="top">

Poll Period \(ms\)

</td>
<td valign="top">

getPeriodInMs

</td>
<td valign="top">

integer

</td>
<td valign="top">

The period in milliseconds between requests of the poll operation.

Default: 1000

</td>
</tr>
<tr>
<td valign="top">

Post Connection

</td>
<td valign="top">

postConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Holds the connection information for the post operation. If a gateway is associated to this connection, it takes precedence over the *Proxy* setting.

-   **Content Type Header** \(ID `contentType`, type `string`\): Post operation content type header \(content-type\).




</td>
</tr>
<tr>
<td valign="top">

Retry Attempts

</td>
<td valign="top">

numRetryAttempts

</td>
<td valign="top">

integer

</td>
<td valign="top">

The number of times to retry a failed request. This applies to all three operations.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Custom Request Connection

</td>
<td valign="top">

customConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

An optional connection to be used by port `inRequest`. If a gateway is associated to this connection, it takes precedence over the *Proxy* setting.

</td>
</tr>
<tr>
<td valign="top">

Proxy

</td>
<td valign="top">

proxy

</td>
<td valign="top">

string

</td>
<td valign="top">

A URL to be used as proxy server. If empty, the system's configuration is used as fallback \(environment variables `HTTP_PROXY`,`http_proxy`,`HTTPS_PROXY`, and `https_proxy`\). This configuration applies to the operations that don't have a gateway associated to their connection.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Request Timeout \(ms\)

</td>
<td valign="top">

requestTimeoutInMs

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of milliseconds to wait for a response before timing out. This applies to all three operations.

Default: 5000

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

The number of milliseconds to wait between consecutive retry attempts. This applies to all three operations.

Default: 0

</td>
</tr>
</table>



<a name="loiof6619b1123794a4fb47fe904859391a2__section_knq_5f3_vdb"/>

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

blob

</td>
<td valign="top">

The data that is sent in a POST request to *Post Connection*. An error is raised if data is received on this port and the connection is not set. The `Content-Type` header is automatically set using the [MIME Sniffing algorithm](https://mimesniff.spec.whatwg.org/).

</td>
</tr>
<tr>
<td valign="top">

`inRequest` 

</td>
<td valign="top">

message

</td>
<td valign="top">

A message specifying a custom HTTP request to be sent. The message **must** contain attribute `http.method` \(the HTTP method for the request\). If attribute `http.url` is not provided, *Custom Request Connection* is used as fallback.

**HTTP Header Fields**:

-   You can set any RFC 7230-compliant HTTP header field by prepending its name with `http.` as a message attribute. For example, when creating a message in a JavaScript operator:

    ```
    message.Attributes["http.Content-Type"] = "text/json";
    ```

    Then, the HTTP Client automatically converts this to

    ```
    Content-Type: text/json
    ```

    in the request's header.

-   Fields `Content-Length`, `Transfer-Encoding`, and `Connection` are added automatically, as needed.
-   If the `Content-Type` header is not set in a message attribute, it is automatically deduced using the [MIME Sniffing algorithm](https://mimesniff.spec.whatwg.org/).
-   Field names are **case-insensitive** \(RFC 7230 -- section 3.2\).



</td>
</tr>
</table>



<a name="loiof6619b1123794a4fb47fe904859391a2__section_swc_cg3_vdb"/>

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

blob

</td>
<td valign="top">

The body of a successful response \(status code in the 2×× range\) received by any operation.

</td>
</tr>
<tr>
<td valign="top">

`outResponse`

</td>
<td valign="top">

message

</td>
<td valign="top">

The complete response given by the server for any operation, including its body as message body.

The message contains the following attributes:

-   `http.status` \(type string\): the returned status \(for example, `"Not Found"`\).
-   `http.statusCode` \(type int\): the code of the returned status \(for example, `200`\).
-   `http.url` \(type string\): the URL of the remote peer.
-   `http.method` \(type string\): the HTTP method \(for example, `GET`\).
-   All HTTP header fields sent by the server, prepended by `http.` \(for example, field `Content-Type` becomes message attribute `http.Content-Type`.



</td>
</tr>
</table>



<a name="loiof6619b1123794a4fb47fe904859391a2__section_vrm_v4d_wdb"/>

## TLS Certificates

The HTTP Client automatically loads and uses all certificate files found under the `/vrep/ca` directory, where all certificates imported into Connection Management are placed.

The operator only recognizes PEM-encoded certificates and ignores other formats.

