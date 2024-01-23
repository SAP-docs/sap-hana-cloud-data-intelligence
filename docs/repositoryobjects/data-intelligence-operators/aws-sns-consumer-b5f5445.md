<!-- loiob5f5445da3e44c66b09effd7a5389f18 -->

# AWS SNS Consumer

Consumes publications from an Amazon Web Services Simple Nodtification Service topic and outputs them as a stream of messages.



<a name="loiob5f5445da3e44c66b09effd7a5389f18__section_rsb_hvh_ghb"/>

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

`connection` 

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory.

An AWS SNS connection consisting of an AWS access key, account ID, key ID, and a region \(defaults to `eu-central-1`\).

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

Name or Amazon Resource Name \(ARN\) of an SNS topic. If only a name is given, an ARN is created using the given region and account ID \(in connection\). The ARN is looked up on SNS. If it does not exist, the consumer fails regardless of the value of `Error handling`.

</td>
</tr>
<tr>
<td valign="top">

Subscription Name

</td>
<td valign="top">

`subscriptionName` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the subscription to create or reuse on the AWS SNS service. The subscription name is used to create a subscription as well as a Simple Queue Service \(SQS\) standard queue which holds matching publications. If the subscription already exists, it is reused.

</td>
</tr>
<tr>
<td valign="top">

Error Handling

</td>
<td valign="top">

`errorHandling` 

</td>
<td valign="top">

string

</td>
<td valign="top">

How the operator handles errors.

Forward: does not fail the graph, Instead the error message is forwarded to output. The output messages have the attribute `message.error` set to true and the attribute `originalMessage` containing the input message that caused the error.

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

Maximum acknowledgment time

</td>
<td valign="top">

`maxAckTime` 

</td>
<td valign="top">

integer

</td>
<td valign="top">

Maximum time period \(in seconds\) between when the consumer receives the message and it sends the acknowledgment to the AWS SNS. If not acknowledged within this period, the SNS service delivers the publication again to the consumer.

If the **Messages to acknowledge** input port is not used, the consumer automatically sends the acknowledgment for a message upon receiving it from the SNS service.

</td>
</tr>
<tr>
<td valign="top">

Maximum message retention time

</td>
<td valign="top">

`maxRetentionPeriod` 

</td>
<td valign="top">

integer

</td>
<td valign="top">

The length of time, in seconds, for which AWS SQS retains a message. Value can be between 60 seconds to 1,209,600 seconds \(14 days\).

</td>
</tr>
<tr>
<td valign="top">

Unsubscribe to topic on shutdown

</td>
<td valign="top">

`unsubscribeOnShutdown` 

</td>
<td valign="top">

boolean

</td>
<td valign="top">

If true, when the graph is shut down, the subscription is removed, which results in no more matching publications being copied to the queue from the topic.

</td>
</tr>
<tr>
<td valign="top">

Remove SQS queue on shutdown

</td>
<td valign="top">

`removeQueueonShutdown` 

</td>
<td valign="top">

boolean

</td>
<td valign="top">

If true, when the graph is shut down, the SQS queue, containing matching publications not consumed yet, is removed.

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



<a name="loiob5f5445da3e44c66b09effd7a5389f18__section_usb_hvh_ghb"/>

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

Messages to acknowledgement

</td>
<td valign="top">

`messageToAck` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The stream of Message IDs. Each publication received by the consumer has a unique ID assigned by the AWS SNS service. Using this ID, the publication can be explicitly acknowledged. The operator reads the message ID from the attribute named `msg.MessageID` in the received message.

</td>
</tr>
</table>



<a name="loiob5f5445da3e44c66b09effd7a5389f18__section_wsb_hvh_ghb"/>

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

Output Messages

</td>
<td valign="top">

`outputMessage` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The stream of publications received by the consumer from the topic on AWS SNS. Each output message contains at least the following three attributes:

-   `msg.MessageID`: a unique ID assigned to each message published to AWS SNS. This ID can be used to explicitly acknowledge a received publication.

-   `msg.TopicArn`: The ARN of the topic that the message was published to.

-   `msg.PublishTime`: The timestamp assigned to the message by AWS SNS.




</td>
</tr>
</table>

