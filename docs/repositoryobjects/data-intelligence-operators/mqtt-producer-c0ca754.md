<!-- loioc0ca754e638c4e6e96f42c726aeda0c9 -->

# MQTT Producer

The MQTT Producer operator receives MQTT messages from a port and publishes them in a topic.



<a name="loioc0ca754e638c4e6e96f42c726aeda0c9__section_sq1_nf3_vdb"/>

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

MQTT brokers

</td>
<td valign="top">

mqttBroker

</td>
<td valign="top">

string

</td>
<td valign="top">

List of MQTT addresses, each separated by a comma. Each broker format should be `scheme://host:port`, where `scheme` is one of the following:

-   `tcp`

-   `ssl`

-   `ws`


Default: "tcp://localhost:1883"

</td>
</tr>
<tr>
<td valign="top">

Topics

</td>
<td valign="top">

topic

</td>
<td valign="top">

string

</td>
<td valign="top">

The category name to which records are published.

Default: "testmqtt/test1"

</td>
</tr>
<tr>
<td valign="top">

Client ID

</td>
<td valign="top">

mqttClientID

</td>
<td valign="top">

string

</td>
<td valign="top">

The client identifier. A clientID must be set. Otherwise, the graph will not run and the ID must be a unique to avoid collision.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Clean session

</td>
<td valign="top">

cleanSession

</td>
<td valign="top">

bool

</td>
<td valign="top">

Set the "clean session" flag in the connect message. This flag indicates that no messages saved by the broker for this client should be delivered.

Default: true

</td>
</tr>
<tr>
<td valign="top">

Insecure skip verify

</td>
<td valign="top">

insecureSkipVerify

</td>
<td valign="top">

bool

</td>
<td valign="top">

Controls whether a client verifies the server's certificate chain and host name.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Retry attempts

</td>
<td valign="top">

retryAttempts

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

Retry period \(ms\)

</td>
<td valign="top">

retryPeriodInMs

</td>
<td valign="top">

int

</td>
<td valign="top">

The time period between each retry attempt in milliseconds.

Default: 1000

</td>
</tr>
<tr>
<td valign="top">

Client connection timeout

</td>
<td valign="top">

timeout

</td>
<td valign="top">

int

</td>
<td valign="top">

Timeout to stabilish connection with client ID.

Default: "500"

</td>
</tr>
<tr>
<td valign="top">

TLS certificate file

</td>
<td valign="top">

tlsCertificateFile

</td>
<td valign="top">

string

</td>
<td valign="top">

The TLS certificate file path.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

TLS key file

</td>
<td valign="top">

tlsKeyFile

</td>
<td valign="top">

string

</td>
<td valign="top">

The TLS key file path.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Username

</td>
<td valign="top">

username

</td>
<td valign="top">

string

</td>
<td valign="top">

The MQTT optional username.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Password

</td>
<td valign="top">

password

</td>
<td valign="top">

string

</td>
<td valign="top">

The MQTT optional password

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Retain message

</td>
<td valign="top">

retainMessage

</td>
<td valign="top">

bool

</td>
<td valign="top">

When set to `true`, the publisher will tell the broker to keep the last message on that topic after consumed.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Explicit message acknowledgement

</td>
<td valign="top">

acknowledgeMessage

</td>
<td valign="top">

bool

</td>
<td valign="top">

When set to `true`, the producer will reconnect every time it receives a new message from the input port. Then it publishs the message to the topics defined and disconnect, sending the status to the `status` output port.

Default: false

</td>
</tr>
</table>



<a name="loioc0ca754e638c4e6e96f42c726aeda0c9__section_knq_5f3_vdb"/>

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

`inmessage` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The stream of records to publish. If the message contains the attribute `mqtt.topic` the message will be published to this topic.

</td>
</tr>
</table>



<a name="loioc0ca754e638c4e6e96f42c726aeda0c9__section_v1k_ylq_vgb"/>

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

`status` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The status after publishing a message \(used when `Explicit message acknowleddgement` is true\). When there is an error, the attribute `error` will have it.

</td>
</tr>
</table>

