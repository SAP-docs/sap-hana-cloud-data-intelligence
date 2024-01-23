<!-- loio582b18896bc14fe4bbd6eaa5e9c1032c -->

# Kafka Consumer V1

The Kafka Consumer operator works as a Kafka client that consumes records or messages from a Kafka cluster. It is compatible with Kafka versions 0.9.x and later.



<a name="loio582b18896bc14fe4bbd6eaa5e9c1032c__section_sq1_nf3_vdb"/>

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

Mandatory. The version of Kafka server being used.

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

Manual: gets connection information from each property.

Connection management: uses connection property for connection information.

Default: "manual"

</td>
</tr>
<tr>
<td valign="top">

Kafka Consumer Connection

</td>
<td valign="top">

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Information about the connection for the service.

</td>
</tr>
<tr>
<td valign="top">

Topics

</td>
<td valign="top">

topics

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the topics from which messages are read and sent to the pipeline \(consumed\). Topic names are separated by `,`.

Default: "test\_topic"

</td>
</tr>
<tr>
<td valign="top">

Auto Set Group ID

</td>
<td valign="top">

autoGroupId

</td>
<td valign="top">

bool

</td>
<td valign="top">

When true, the group ID is set according to the multiplicity index of the operator. For instance, when the operator is inside a group with multiplicity = 3, each node consumes from `group-0`,`group-1` and `group-2`, where `group` is the value set in `groupID` config and `-*` is the multiplicity index.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Auto Commit

</td>
<td valign="top">

autoCommit

</td>
<td valign="top">

bool

</td>
<td valign="top">

Whether to automatically commit the message \(mark message as processed\). When this configuration is enabled, each message is committed right after it is sent to the output port. Once a message is committed, it will not be consumed anymore, and it is removed from the queue.

Default: true

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

The maximum number of message bytes to fetch from the broker in a single request.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Max Wait Time

</td>
<td valign="top">

maxWaitTime

</td>
<td valign="top">

int

</td>
<td valign="top">

The maximum amount of time in milliseconds that the broker waits for the consumer.

Default: 500

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

Offset

</td>
<td valign="top">

offset

</td>
<td valign="top">

string

</td>
<td valign="top">

The initial offset to use if no offset was previously commited.

Default: "newest"

</td>
</tr>
<tr>
<td valign="top">

Maintain Full Metada Set

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
<tr>
<td valign="top">

Terminate on Error

</td>
<td valign="top">

terminateOnError

</td>
<td valign="top">

bool

</td>
<td valign="top">

Whether to terminate the consumer in case the Kafka Consumer throws an error.

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

Type of connection: Manual \(user input\) or retrieved by the Connection Management Service.

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

Kafka Consumer Connection

</td>
<td valign="top">

According to connection property

</td>
<td valign="top">

object

</td>
<td valign="top">

All the connection properties for manual input:

*Brokers* \(ID brokers, type string\). Mandatory. The list of nodes in the cluster following the format 'host:port' and separated by commas. Default: "localhost:9092"

*Group ID* \(ID groupID, type string\). Mandatory. All information for a consumer that is part of the group. Default: "test\_group"

*Use TLS* \(ID useTLS, type bool\). Flag that enables TLS/SSL authentication. Default: false

*Insecure Skip Verify* \(ID insecureSkipVerify, type bool\). If a client verifies the server's certificate chain and host name. Default: false

*Use Certificate Authority* \(ID useCA, type bool\). If this property is true, the TLS CA file is requested.

> ### Note:  
> only enabled when 'Use TLS' is true.

Default: true

*Certificate Authority Path* \(ID tlsCAFile, type string\). Server's certificate authority file path \(extension has to be .pem\). Default: ""

*Client Certificate Path* \(ID tlsClientCertFile, type string\). Client certificate file that is loaded with public or private key pair if applicable \(extension has to be .pem\). Default: ""

*Client Key Path* \(ID tlsClientKeyFile, type string\). Client key file that is loaded with client certificate file if applicable \(extension has to be .pem\).

> ### Note:  
> the supported encryption key types are: rsa, ecdsa and ed25519.

Default: ""

*Authentication* \(ID authenticate, type bool\). Manual configuration: flag that enables SASL authentication. Default: false

*Username* \(ID username, type string\). Username if using Kafka's SASL/PLAIN authentication. Default: ""

*Password* \(ID password, type string\). Password if using Kafka's SASL/PLAIN authentication. Default: ""

*SASL Authentication* \(ID saslAuthentication, type string\). Authentication mechanism to be used.

> ### Note:  
> PLAIN, SCRAM-256, SCRAM-512, and GSSAPI for Kerberos are supported \(the property is considered only if username and password are set, except for GSSAPI\).

Default: "PLAIN"

*Kafka Kerberos Service Name* \(ID serviceNameGSSAPI, type string\). Service name defined for the kerberized Kafka server. Default: "kafka"

*Kafka Kerberos Realm* \(ID realmGSSAPI, type string\). Realm defined for the kerberized Kafka server. Default: ""

*Authentication Type for Kafka/GSSAPI* \(ID authTypeGSSAPI, type string\). Authentication type for Kafka/GSSAPI, when "User/password" is used, username and password must be set, when "Keytab file authentication" is used, keytab path must be set. Default: "User/Password Authentication"

*Kerberos Config Path* \(ID kerberosConfigPath, type string\). Kerberos configuration path \(krb5.conf file\). Default: ""

*Keytab File Path* \(ID keytabPath, type string\). Path for keytab file for Kafka client. Default: ""

</td>
</tr>
</table>



<a name="loio582b18896bc14fe4bbd6eaa5e9c1032c__section_knq_5f3_vdb"/>

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

`markoffsets` 

</td>
<td valign="top">

message

</td>
<td valign="top">

An offset \(record\) of the provided topic or partition as processed \(committed\) the header `message.commit.token` must be set.

</td>
</tr>
</table>



<a name="loio582b18896bc14fe4bbd6eaa5e9c1032c__section_swc_cg3_vdb"/>

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

`message` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The stream of records consumed.

</td>
</tr>
<tr>
<td valign="top">

`event`

</td>
<td valign="top">

message

</td>
<td valign="top">

The stream of events produced by the consumer such as consumer rebalance notifications.

</td>
</tr>
</table>

