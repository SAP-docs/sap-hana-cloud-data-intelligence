<!-- loio2d49acedfb33494aaee6d2ccaf1758b7 -->

# AWS SNS Producer

Receives a message from the input port and publishes it to an Amazon Web Services Simple Nodtification Service topic.



SNS accepts only string as the body of the message. If the input message has a non-string body, it will be encoded using Base64, encoding to a string, and an attribute named `msg.IsSnsBodyEncoded` with the value `true`, is added to the SNS message. If the SNS message is consumed via the corresponding consumer, decoding the body and removing the `msg.IsSnsBodyEncoded` attribute is done automatically.



<a name="loio2d49acedfb33494aaee6d2ccaf1758b7__section_rsb_hvh_ghb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Parameter

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

`connection` 

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory.

An AWS SNS connection consisting of an AWS access key, account ID and key ID.

</td>
</tr>
<tr>
<td valign="top">

Topic

</td>
<td valign="top">

`topic` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Name or Amazon Resource Name \(ARN\) of an SNS topic. If only a name is given, an ARN is created using the given region and account ID \(in connection\). The ARN is looked up on SNS. If it already exists, it gets reused. If not, it will be created. The provided topic is the default topic that received messages will be published to.

Alternatively, if there exists a `msg.TopicArn` attribute in the message, the value of this attribute is used as topic name and the message is published to this topic rather than topic. This attribute will also exist in the message received by the consumer. If topic is empty and the producer cannot get the topic name from the message attributes, the producer fails regardless of the value of `Error handling`.

</td>
</tr>
<tr>
<td valign="top">

Error handling

</td>
<td valign="top">

`errorHandling` 

</td>
<td valign="top">

string

</td>
<td valign="top">

How the operator handles errors.

Forward: does not fail the graph, instead the error message is forwarded to output. The output messages have the attribute`message.error` set to true and the attribute `originalMessage` containing the input message that caused the error.

Fail: fails the graph upon error.

Ignore: only prints a warning in the log and ignores the error.

</td>
</tr>
<tr>
<td valign="top">

Maximum retries

</td>
<td valign="top">

`maxRetries` 

</td>
<td valign="top">

integer

</td>
<td valign="top">

Refers to the number of retries performed by the operator when sending a request to the SNS API.

</td>
</tr>
<tr>
<td valign="top">

Delete topic on shutdown

</td>
<td valign="top">

`deleteTopicOnShutdown` 

</td>
<td valign="top">

boolean

</td>
<td valign="top">

If true, when the graph is shut down, the SNS topic is deleted. Currently, SNS deletes all attached subscriptions as well.

</td>
</tr>
<tr>
<td valign="top">

Proxy

</td>
<td valign="top">

`proxy` 

</td>
<td valign="top">

string

</td>
<td valign="top">

HTTP proxy to be used by the HTTP client issuing SNS API calls.

</td>
</tr>
</table>



<a name="loio2d49acedfb33494aaee6d2ccaf1758b7__section_usb_hvh_ghb"/>

## Input


<table>
<tr>
<th valign="top">

Input

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

Messages to publish

</td>
<td valign="top">

`messageToPublish` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The stream of records to publish. If the input messages have `message.error` set to true, the behavior is based on the value of `Error Handling`.

Messages must be UTF-8 encoded strings at most 256 KB in size. Message must have a body. An empty body is replaced with "".

An SNS message with an empty string as its body, will be converted to a Modeler message with nil as its body. The message body must either a string or a byte array.

</td>
</tr>
</table>



<a name="loio2d49acedfb33494aaee6d2ccaf1758b7__section_wsb_hvh_ghb"/>

## Output


<table>
<tr>
<th valign="top">

Output

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

Publishing results

</td>
<td valign="top">

`publishResult` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The result of publishing an input message is written to this output either as a successful publication, which would include assigned message ID for the publication \(by SNS\) and the topic it was published to, under the attributes `msg.MessageID` and `msg.TopicArn`, respectively.

</td>
</tr>
</table>

