<!-- loio709a1b65b93d4f5f90c992b3442f92ab -->

# MQTT Consumer

The MQTT Consumer operator subscribes to MQTT topics, consumes its messages, and outputs them.





<a name="loio709a1b65b93d4f5f90c992b3442f92ab__section_sq1_nf3_vdb"/>

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

mqttbroker

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

Topic

</td>
<td valign="top">

topic

</td>
<td valign="top">

string

</td>
<td valign="top">

The topic name to which consumer will subscribe.

Default: "testmqtt/test1"

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

Will set the "clean session" flag in the connect message. This flag indicates that no messages saved by the broker for this client should be delivered.

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

Client ID

</td>
<td valign="top">

mqttClientID

</td>
<td valign="top">

string

</td>
<td valign="top">

The client identifier.

Default: "mqttConsumer"

</td>
</tr>
<tr>
<td valign="top">

Retry attempts

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

The MQTT optional username

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

Explicit request mode

</td>
<td valign="top">

explicitRequestMode

</td>
<td valign="top">

bool

</td>
<td valign="top">

When set to `true`, this property changes the way that consumer deals with messages. It will wait for an input of `singlemessagerequest` port to connect a client, consume only one message from it, and then disconnect the client. This cycle happens whenever a signal comes through `singlemessagerequest`.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Timeout \(s\)

</td>
<td valign="top">

timeout

</td>
<td valign="top">

int

</td>
<td valign="top">

In case that explicit request mode is being used, this property is the time to wait to receive a message.

Default: 15

</td>
</tr>
</table>



<a name="loio709a1b65b93d4f5f90c992b3442f92ab__section_nrv_lkq_vgb"/>

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

`singlemessagerequest` 

</td>
<td valign="top">

message

</td>
<td valign="top">

This input port should be used when `explicitRequestMode` is set to true. The input message can be empty or include the attribute `mqtt.topic`. After receiving the signal, the MQTT client will connect, subscribe to topic, consume one message, and disconnect.

</td>
</tr>
</table>



<a name="loio709a1b65b93d4f5f90c992b3442f92ab__section_swc_cg3_vdb"/>

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

`outmessage` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The stream of records published.

</td>
</tr>
</table>

