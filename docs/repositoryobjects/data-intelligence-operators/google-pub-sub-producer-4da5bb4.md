<!-- loio4da5bb4ee96a4893b17e75fba77b7582 -->

# Google Pub/Sub Producer

Receives a message from the input port and publishes it to a Google Pub/Sub topic.



-   The provided *Topic* is the default topic that received messages will be published to. Alternatively, if a`gcp.pubsub.topicName` attribute exists in the message, the value of this attribute is used as topic name and the message is published to this topic rather than *Topic*. This attribute will not be removed by the producer upon publish. If *Topic* is empty and the producer cannot get the topic name from the message attributes, the producer fails regardless of the value of*Fail on error*.
-   *Create topic if it does not exist* applies only to *Topic*, not topic names mentioned in the message attributes.
-   If *Fail on error*is false, upon error, the producer only outputs the error message on *Error* output port and does not fail the graph. The message to be published is discarded.
-   *Subscription name to create* applies only to *Topic* and not topic names mentioned in the message attributes. If specified, the producer makes sure the subscription to *Topic* exists \(if not, it creates the subscription\) on Google Pub/Sub before processing input messages. Creating a subscription before publishing can ensure publications published to *Topic* are stored on Google Pub/Sub, even if at the time of publishing, no subscription to *Topic* exists. Google Pub/Sub does not guarantee storing undelivered publications when there are on matching subscriptions.
-   If the number of publications received by the producer, but not yet published to the Google Pub/Sub service is more than *Maximum outstanding publications*, the producer does not process messages from *messageToPublish* input until one or more messages are finished publishing. Publishing a message is finished when the producer outputs its message ID on the *publishedMessage* output port, or an error occurs and the error is written to the *error* output port.
-   Upon publish timeout, an error message is written to the *error* output port and if *Fail on error* is true, the graph fails.
-   The encoding of the received input message is stored in an attribute named `message.encoding` in the message published to the Google Pub/Sub service. The Google Pub/Sub consumer uses this attribute to reconstruct the same SAP Data Intelligence message.
-   As Google Pub/Sub supports only string as a key or value type of attributes, any attribute included in the input message to this operator must have strings as key and value.
-   To improve the throughput of the operator, publications are batched. The value of *Publication batch size* must be smaller than *Maximum outstanding publications*. This is checked by the producer upon initialization.



<a name="loio4da5bb4ee96a4893b17e75fba77b7582__section_lr4_xrw_cfb"/>

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

Mandatory. A Google Pub/Sub connection consisting of a Google Cloud Platform \(GCP\) project ID and a JSON key file to access the Pub/Sub service.

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

Create topic if it does not exist

</td>
<td valign="top">

createTopicIfNotExists

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Whether to create *Topic* if it does not exist on the given Google Pub/Sub project.

Default: true

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

Whether to fail the whole graph if the producer encounters an error at runtime.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Subscription Name to Create

</td>
<td valign="top">

subscriptionName

</td>
<td valign="top">

string

</td>
<td valign="top">

Ensure that the given subscription name exists for *Topic*.

</td>
</tr>
<tr>
<td valign="top">

Maximum Outstanding Publications

</td>
<td valign="top">

maxOutstandingPubs

</td>
<td valign="top">

integer

</td>
<td valign="top">

Maximum number of publications that are submitted to the operator but are not finished being published.

Default: 1000

</td>
</tr>
<tr>
<td valign="top">

Publish Timeout \(sec\)

</td>
<td valign="top">

publishTImeout

</td>
<td valign="top">

integer

</td>
<td valign="top">

Maximum timeout in seconds for publishing a publication.

Default: 60

</td>
</tr>
<tr>
<td valign="top">

Publication Batch Size

</td>
<td valign="top">

publishBatchSize

</td>
<td valign="top">

integer

</td>
<td valign="top">

Minimum number of publications that the producer needs to receive before sending a batch of publications to the Google Pub/Sub service.

Default: 100

</td>
</tr>
<tr>
<td valign="top">

Delay Between Retrying Failed Publications \(msec\)

</td>
<td valign="top">

retryDelay

</td>
<td valign="top">

integer

</td>
<td valign="top">

Time to wait before retrying a failed publication.

Default: 1000

</td>
</tr>
<tr>
<td valign="top">

Number of Retry Attempts for Failed Publications

</td>
<td valign="top">

retryAttempts

</td>
<td valign="top">

integer

</td>
<td valign="top">

Maximum number of retries for a failed publication. Upon reaching this limit, an error is generated and handled according to the value of *Fail on error*.

Default: 5

</td>
</tr>
</table>



<a name="loio4da5bb4ee96a4893b17e75fba77b7582__section_s1d_wtw_cfb"/>

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

`messageToPublish` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The stream of messages to publish.

</td>
</tr>
</table>



<a name="loio4da5bb4ee96a4893b17e75fba77b7582__section_dfm_c5w_cfb"/>

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

`publishedMessage` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Upon successful publication, Google Pub/Sub assigns a unique ID to each publication. The producer outputs these IDs as a steam of messages on this port, with the message ID as value of the attribute `msg.MessageID`.

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

Error messages occurring during runtime are output on this port as a stream of message \(one for each error\). The error message has the attribute `msg.KeyError` with the value `true` and for errors relating to publishing a message, the original message can be retrieved using the attribute `originalMessage`. The body of the message is the error message.

</td>
</tr>
</table>

