<!-- loioe22d0e5f8f564a76a1fe0486845b0303 -->

# Kafka Producer V2

The Kafka Producer operator allows applications to send records or messages to topics on a Kafka cluster. It is compatible with Kafka versions 0.8.x and later.



<a name="loioe22d0e5f8f564a76a1fe0486845b0303__section_sq1_nf3_vdb"/>

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

Mandatory. The object containing the connection parameters to a KAFKA instance.

Default: \{\}

</td>
</tr>
<tr>
<td valign="top">

Kafka Version

</td>
<td valign="top">

kafkaVersion

</td>
<td valign="top">

string

</td>
<td valign="top">

Version of Kafka server being used.

Default: "1.0.0"

</td>
</tr>
<tr>
<td valign="top">

Topic

</td>
<td valign="top">

topics

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The category name to which records are subscribed. A new topic name can be set using the `kafka.topic` message attribute for port `message`.

Default: "test\_topic"

</td>
</tr>
<tr>
<td valign="top">

Validate Topic Existence

</td>
<td valign="top">

checkTopic

</td>
<td valign="top">

bool

</td>
<td valign="top">

Specifies whether the operator should validate that the topic from configuration exists during initialization.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Manual Partitioning

</td>
<td valign="top">

manualPartitioning

</td>
<td valign="top">

bool

</td>
<td valign="top">

Specifies whether the partition is configured manually, it means that the user chooses the partition of the message.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Partition

</td>
<td valign="top">

partition

</td>
<td valign="top">

int

</td>
<td valign="top">

Determines the message's partition when `Manual Partitioning` is set to true. Any value greater than or equal to 0 is considered as a valid partition.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Key

</td>
<td valign="top">

key

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines the message's partition key when the property `manualPartitioning` is set to false.

Default: ""

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

int

</td>
<td valign="top">

The number of attempts to retry.

Default: 0

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

The retry waiting time in milliseconds.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Async

</td>
<td valign="top">

async

</td>
<td valign="top">

bool

</td>
<td valign="top">

Specifies whether the producer should work on asynchronous mode. If true, the operator starts an asynchronous publishing operation for each input. If false, input processing only finishes when the message is acknowledged by the Kafka server. This affects the snapshot behavior. See the section **Snapshot Support** for details.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Transaction Timeout \(seconds\)

</td>
<td valign="top">

txnTimeout

</td>
<td valign="top">

int

</td>
<td valign="top">

Maximum duration that the broker will wait for a transaction commit. It is effective only when a graph is executed with snapshot enabled. Its value has to be higher than the graph's snapshot interval, but cannot exceed the `transaction.max.timeout.ms` configuration from Kafka Server side.

Default: 600

</td>
</tr>
<tr>
<td valign="top">

Compression Format

</td>
<td valign="top">

compressionFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

Specifies the type of compression to use on messages. Options are: "No compression", "GZIP", "Snappy", "LZ4", and "Zstandard". The Zstandard format is supported only by Kafka version 2.1.0 or above, as specified at [Kafka Documentation](https://kafka.apache.org/documentation/).

Default: "No Compression"

</td>
</tr>
<tr>
<td valign="top">

Max Message \(bytes\)

</td>
<td valign="top">

maxMessageBytes

</td>
<td valign="top">

int

</td>
<td valign="top">

The maximum allowed size of a message. Limited to at most 100 MiB, which is the largest request the broker will attempt to process.

Default: 1000000

</td>
</tr>
<tr>
<td valign="top">

Max Message Batch

</td>
<td valign="top">

maxMessageBatch

</td>
<td valign="top">

int

</td>
<td valign="top">

The maximum number of messages the producer will send in a single broker request. Defaults to 0 for unlimited.

Default: 0

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

The maximum duration the broker will wait the receipt of the number of required acks \(defaults to 30 seconds\).

Default: 30000

</td>
</tr>
<tr>
<td valign="top">

Maintain Full Metadata Set

</td>
<td valign="top">

fullMetadataSet

</td>
<td valign="top">

bool

</td>
<td valign="top">

Whether to maintain a full set of metadata for all topics in the Kafka cluster os just the minimal set necessary. If there are many topics or partitions, it is recommended to disable this option.

Default: true

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

Whether to terminate the consumer in case the Kafka Consumer throws an error.

Default: "terminate on error"

</td>
</tr>
</table>



<a name="loioe22d0e5f8f564a76a1fe0486845b0303__section_knq_5f3_vdb"/>

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

message

</td>
<td valign="top">

message

</td>
<td valign="top">

A binary input whose body is used as the content to be produced. The `topic` and `partition`/`key` values from the com.sap.headers.kafka header may be used as well, according to the operator configuration. Note that `partition` from input takes precedence over the `partition` from config, which in turn takes precedence over the `key`. And `key` from input takes precedence over key from config.

</td>
</tr>
</table>



<a name="loioe22d0e5f8f564a76a1fe0486845b0303__section_swc_cg3_vdb"/>

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

out

</td>
<td valign="top">

message

</td>
<td valign="top">

It depends on the following:

-   Operator running with snapshot: An empty output, after each successful commit, containing the com.sap.headers.kafka.produced header.
-   Operator running without snapshot: An empty output, after each successful message, containing the com.sap.headers.kafka header.



</td>
</tr>
<tr>
<td valign="top">

error

</td>
<td valign="top">

message

</td>
<td valign="top">

An error message.

</td>
</tr>
</table>



<a name="loioe22d0e5f8f564a76a1fe0486845b0303__section_rnt_r5v_nsb"/>

## Snapshot Support

Snapshot support is provided when `Async` is set to **True**. That way, all messages are grouped as part of a transaction and are committed only when the next snapshot completes. Currently, `metadata` and `headers` received on input are not replicated to the Kafka server if this feature is enabled.

