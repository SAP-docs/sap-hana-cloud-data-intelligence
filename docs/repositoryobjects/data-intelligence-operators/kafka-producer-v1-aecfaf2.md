<!-- loioaecfaf2967114d01b1afbc7eabdc0989 -->

# Kafka Producer V1

The Kafka Producer operator allows applications to send records or messages to topics on a Kafka cluster. It is compatible with Kafka versions 0.8.x and later.



<a name="loioaecfaf2967114d01b1afbc7eabdc0989__section_sq1_nf3_vdb"/>

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

Connection Type

</td>
<td valign="top">

connectionType

</td>
<td valign="top">

string

</td>
<td valign="top">

*manual*: gets connection information from each property.

*connection management*: uses connection property for connection information.

Default: "manual"

</td>
</tr>
<tr>
<td valign="top">

Kafka Producer Connection

</td>
<td valign="top">

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Holds information about the connection for the service.

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

Key

</td>
<td valign="top">

key

</td>
<td valign="top">

string

</td>
<td valign="top">

The key to be included in the record. A new key can also be set using the `kafka.key` message attribute for port `message` when the property `manualPartitioning` is false.

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

Partition

</td>
<td valign="top">

partition

</td>
<td valign="top">

int

</td>
<td valign="top">

The partition count.

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

Specifies whether the producer should work on asynchronous mode. If true, the operator starts an asynchronous publishing operation for each input. If false, input processing only finishes when the message is acknowledged by the Kafka server.

Default: false

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

Whether to maintain a full set of metadata for all topics in the Kafka cluster or just the minimal set necessary. If there are many topics and partitions, it is recommended to disable this option.

Default: true

</td>
</tr>
</table>

**Connection Parameters**


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

Configuration Type

</td>
<td valign="top">

configurationType

</td>
<td valign="top">

string

</td>
<td valign="top">

Type of connection information that is used: Manual \(user input\) or retrieved by the Connection Management Service.

Default: "Configuration manager"

</td>
</tr>
<tr>
<td valign="top">

Connection ID

</td>
<td valign="top">

connectionID

</td>
<td valign="top">

string

</td>
<td valign="top">

The ID of the connection information to be retrieved from the Connection Management Service.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Kafka Producer Connection

</td>
<td valign="top">

According to connection properties.

</td>
<td valign="top">

object

</td>
<td valign="top">

All the connection properties for manual input:

*Brokers* \(ID `brokers`, type `string`\). Mandatory. The list of nodes in the cluster following the format 'host:port' and separated by commas. Default: "localhost:9092"

*Use TLS* \(ID `useTLS`, type `bool`\). Flag that enables using TLS/SSL authentication. Default: false

*Insecure Skip Verify* \(ID `insecureSkipVerify`, type `bool`\). If a client verifies the server's certificate chain and host name. Default: false

*Use Certificate Authority* \(ID `useCA`, type `bool`\). If this property is true, the TLS CA file is requested.

> ### Note:  
> Only enabled when 'Use TLS' is true.

If the certificate is uploaded to connection management, the path should be set as `/vrep/vflow`. Default: true

*Certificate Authority Path* \(ID `tlsCAFile`, type `string`\). Server's certificate authority file path \(extension has to be .pem\). Default: ""

*Client Certificate Path* \(ID `tlsClientCertFile`, type `string`\). Client certificate file that is loaded with public or private key pair if applicable \(extension has to be .pem\). Default: ""

*Client Key Path* \(ID `tlsClientKeyFile`, type `string`\). Client key file that will be loaded with client certificate file if applicable \(extension has to be .pem\). Note: the supported encryption key types are: rsa, ecdsa, and ed25519. For instance, with Java keystore, the -keyalg RSA constraint should be used. Default: ""

*Authentication* \(ID `authenticate`, type `bool`\). Manual configuration. Flag that enables SASL authentication. Default: false

*Username* \(ID `username`, type `string`\). Username if using Kafka's SASL/PLAIN authentication. Default: ""

*Password* \(ID `password`, type `string`\). Password if using Kafka's SASL/PLAIN authentication. Default: ""

*SASL Authentication* \(ID `saslAuthentication`, type `string`\). Authentication mechanism to be used. Note: PLAIN, SCRAM-256, and SCRAM-512 are supported \(the property is considered only if username and password are set\). Default: "PLAIN"

*Kafka Kerberos Service Name* \(ID `serviceNameGSSAPI`, type `string`\). Service name defined for the kerberized Kafka server. Default: "kafka"

*Kafka Kerberos Realm* \(ID `realmGSSAPI`, type `string`\). Realm defined for the kerberized Kafka server. Default: ""

*Authentication Type for Kafka/GSSAPI* \(ID `authTypeGSSAPI`, type `string`\). Authentication type for Kafka/GSSAPI, when "User/password" is used, username and password must be set; when "Keytab file authentication" is used, keytab path must be set. Default: "User/Password Authentication"

*Kerberos Config Path* \(ID `kerberosConfigPath`, type `string`\). Kerberos configuration path \(krb5.conf file\). Default: ""

*Keytab File Path*

\(ID `keytabPath`, type `string`\). Path for keytab file for Kafka client. Default: ""

</td>
</tr>
</table>



<a name="loioaecfaf2967114d01b1afbc7eabdc0989__section_knq_5f3_vdb"/>

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

The stream of records to publish.

</td>
</tr>
</table>



<a name="loioaecfaf2967114d01b1afbc7eabdc0989__section_swc_cg3_vdb"/>

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

markoffsets

</td>
<td valign="top">

message

</td>
<td valign="top">

Message containing the offsets marked as part of the current transaction and set of headers.

</td>
</tr>
</table>

