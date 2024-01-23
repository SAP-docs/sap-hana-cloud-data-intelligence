<!-- loio36aa260d17f54d738071b9c7a716faea -->

# Rest API Client

The Rest API Client operator performs HTTP requests according to its configurations and provided inputs.



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

Retry Attempts

</td>
<td valign="top">

retries

</td>
<td valign="top">

integer

</td>
<td valign="top">

The number of times to retry a request that returned a `5xx` status code in the response.

This configuration does not apply to other status code\(s\) or failed request executions.

Default: `0`

</td>
</tr>
<tr>
<td valign="top">

Retry Interval \(ms\)

</td>
<td valign="top">

retryInterval

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of milliseconds to wait between consecutive retry attempts.

Default: `0`

</td>
</tr>
<tr>
<td valign="top">

Request Timeout \(ms\)

</td>
<td valign="top">

timeout

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of milliseconds to wait for a response before timing out. This applies to all three operations.

Default: `5000`

</td>
</tr>
<tr>
<td valign="top">

Error Handling

</td>
<td valign="top">

errorHandling

</td>
<td valign="top">

string

</td>
<td valign="top">

Details available at [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:.

Default: `"terminate on error"`

</td>
</tr>
</table>



<a name="loio36aa260d17f54d738071b9c7a716faea__section_hyc_mqf_gxb"/>

## Input


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Kind

</th>
<th valign="top">

Type ID

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

request

</td>
<td valign="top">

scalar

</td>
<td valign="top">

com.sap.core.binary

</td>
<td valign="top">

The request body to be sent, together with the header `com.sap.headers.http.request` specifying the request attributes.

In regards to the header list from input, the keys are canonicalized to have the first letter in **uppercase**.

> ### Example:  
> Input value:
> 
> Key: `content-type` / Value: `application/json`
> 
> Resulting header in the HTTP request:
> 
> Key: `Content-Type` / Value: `application/json`



</td>
</tr>
</table>



<a name="loio36aa260d17f54d738071b9c7a716faea__section_sfc_frf_gxb"/>

## Output

****


<table>
<tr>
<th valign="top">

Output

</th>
<th valign="top">

Kind

</th>
<th valign="top">

Type ID

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

response

</td>
<td valign="top">

scalar

</td>
<td valign="top">

com.sap.core.binary

</td>
<td valign="top">

The body of the HTTP response, together with the header `com.sap.headers.http.response` containing its details.

</td>
</tr>
<tr>
<td valign="top">

error

</td>
<td valign="top">

structure

</td>
<td valign="top">

com.sap.error

</td>
<td valign="top">

An error message, if applicable, as described at [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:.

</td>
</tr>
</table>



<a name="loio36aa260d17f54d738071b9c7a716faea__section_el1_rrf_gxb"/>

## Snapshot Support

The operator has no internal state, but when the graph is executed with `Snapshot` enabled, it is stateful by default, meaning that the states are saved only when it successfully handles the received input\(s\).

