<!-- loio68835e22b134457485f365ea967c203d -->

# Google Pub/Sub Consumer

Consumes publications from a Google Pub/Sub topic and outputs them as a stream of messages.



-   If *Subscription name* refers to an existing subscription name on the Google Pub/Sub service, *Topic* can be empty, as an existing subscription is already attached to a topic. If subscription is to be created, *Topic* must be provided and *Topic* must exist on the Pub/Sub service. Otherwise, the graph fails regardless of the value of *Fail on error*.

-   If *Fail on error*is false, upon error, the consumer only outputs the error message on *Error* output port and does not fail the graph.

-   The *messageToAck* input port is optional. If connected, no automatic acknowledgment is sent and the user has to explicitly acknowledge received publications by submitting their message ID to this port. This allows using the Google Pub/Sub service as a message queue and ensures that publications that are not consumed successfully get delivered again to the same consumer or other consumers using the same *Subscription name*.

-   When using explicit acknowledgment, receiving more than one ack for the same publication or requesting acknowledgment for a publication that is not received by the consumer results in an error.




<a name="loio68835e22b134457485f365ea967c203d__section_sq1_nf3_vdb"/>

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

string

</td>
<td valign="top">

Mandatory. A Google Pub/Sub connection consisting of a GCP project ID and a JSON key file to access the Pub/Sub service.

</td>
</tr>
<tr>
<td valign="top">

Subscription Name

</td>
<td valign="top">

subscriptionName

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The name of the subscription on the Google Pub/Sub service.

</td>
</tr>
<tr>
<td valign="top">

Topic

</td>
<td valign="top">

topic

</td>
<td valign="top">

string

</td>
<td valign="top">

Google Pub/Sub topic name.

</td>
</tr>
<tr>
<td valign="top">

Fail on Error

</td>
<td valign="top">

failOnError

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Whether to fail the whole graph if the consumer encounters an error at runtime.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Maximum Acknowledgment Time \(sec\)

</td>
<td valign="top">

maxAckExtension

</td>
<td valign="top">

integer

</td>
<td valign="top">

Maximum time period between when the consumer receives the message and it sends the acknowledgment to the Google Pub/Sub service. If not acknowledged within this period, the Pub/Sub service delivers the publication again to the same consumer or any other consumer that is configured to use the same Subscription name. If the messageToAck input port is not used, the consumer automatically sends the acknowledgment for a message upon receiving it from the Pub/Sub service.

Default: 600

</td>
</tr>
<tr>
<td valign="top">

Maximum Outstanding Publications

</td>
<td valign="top">

maxOutsandingMessages

</td>
<td valign="top">

integer

</td>
<td valign="top">

Maximum number of received but unacknowledged messages on the consumer. Upon reaching this maximum, the consumer stops pulling publications form the Pub/Sub service until one or more of the existing messages expire \(ack deadline is passed\) or acknowledged. A negative value indicates no limit for the number of unprocessed messages.

Default: 1000

</td>
</tr>
<tr>
<td valign="top">

Synchronously pull messages

</td>
<td valign="top">

synchronousPull

</td>
<td valign="top">

boolean

</td>
<td valign="top">

If set, pull messages synchronously ensuring the buffer does not exceed the maximum outstanding messages. Otherwise, asynchronously pull messages as determined by the operator, not guaranteeing the maximum outstanding messages limit. Therefore, setting this configuration to true is the only way to guarantee that buffered unprocessed messages on the consumer do not exceed maximum outstanding messages.

Default: False

</td>
</tr>
</table>



<a name="loio68835e22b134457485f365ea967c203d__section_knq_5f3_vdb"/>

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

`messageToAck` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Messages to be acknowledged. The stream of Message IDs. Each publication received by the consumer has a unique ID assigned by the Google Pub/Sub service. Using this ID, the publication can be explicitly acknowledged. The operator reads the message ID from the attribute named `msg.MessageID` in the received message.

</td>
</tr>
</table>



<a name="loio68835e22b134457485f365ea967c203d__section_swc_cg3_vdb"/>

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

`receivedMessage` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The stream of publications received by the consumer from the Topic on Google Pub/Sub service. Each output message contains the following extra two attributes:

-   `gcp.pubsub.message.ID`: a unique ID assigned to each message published to Google Pub/Sub. This ID can be used to explicitly acknowledge a received publication.

-   `gcp.pubsub.message.publishTime`: The timestamp assigned to the message by the Google Pub/Sub service upon its publication.




</td>
</tr>
<tr>
<td valign="top">

`error`

</td>
<td valign="top">

message

</td>
<td valign="top">

Error messages occurring during runtime are output on this port as a stream of messages \(one for each error\). The error message has the attribute `msg.KeyError` with the value `true` and the body of the message is the error message.

</td>
</tr>
</table>

