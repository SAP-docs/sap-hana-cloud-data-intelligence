<!-- loiob12fb5d7a451425986ebc6a67ba99b0f -->

# Connectivity

-   **[AWS SNS Consumer](aws-sns-consumer-b5f5445.md "Consumes publications from an Amazon Web Services Simple Nodtification Service topic and
		outputs them as a stream of messages.")**  
Consumes publications from an Amazon Web Services Simple Nodtification Service topic and outputs them as a stream of messages.
-   **[AWS SNS Producer](aws-sns-producer-2d49ace.md "Receives a message from the input port and publishes it to an Amazon Web Services Simple
		Nodtification Service topic.")**  
Receives a message from the input port and publishes it to an Amazon Web Services Simple Nodtification Service topic.
-   **[Google Pub/Sub Consumer](google-pub-sub-consumer-68835e2.md "Consumes publications from a Google Pub/Sub topic and outputs them as a stream of
		messages.")**  
Consumes publications from a Google Pub/Sub topic and outputs them as a stream of messages.
-   **[Google Pub/Sub Producer](google-pub-sub-producer-4da5bb4.md "Receives a message from the input port and publishes it to a Google Pub/Sub
		topic.")**  
Receives a message from the input port and publishes it to a Google Pub/Sub topic.
-   **[Receive Email](receive-email-f065059.md "Receives emails. The protocol used is IMAP Version 4rev1. The operator fetches emails
		automatically if the in port is not connected. When the port is connected, the operator
		fetches emails whenever a new entry arrives. The output is received as single messages, each
		related to a single email.")**  
Receives emails. The protocol used is IMAP Version 4rev1. The operator fetches emails automatically if the in port is not connected. When the port is connected, the operator fetches emails whenever a new entry arrives. The output is received as single messages, each related to a single email.
-   **[Send Email](send-email-8da19b1.md "Sends e-mails. It uses an SMTP protocol. Every time data comes through the input port, a
		new e-mail is built and sent.")**  
Sends e-mails. It uses an SMTP protocol. Every time data comes through the input port, a new e-mail is built and sent.
-   **[HTTP Client](http-client-f6619b1.md "The HTTP Client operator performs HTTP requests.")**  
The HTTP Client operator performs HTTP requests.
-   **[HTTP Server](http-server-8677737.md "This operator allows a graph to accept HTTP requests on user-defined endpoints (routes)
		and respond to them based on messages produced on the fly by other operators in the
		graph.")**  
This operator allows a graph to accept HTTP requests on user-defined endpoints \(routes\) and respond to them based on messages produced on the fly by other operators in the graph.
-   **[Kafka Consumer V1](kafka-consumer-v1-582b188.md "The Kafka Consumer operator works as a Kafka client that consumes records or messages from a Kafka cluster. It is compatible with Kafka
		versions 0.9.x and later.")**  
The Kafka Consumer operator works as a Kafka client that consumes records or messages from a Kafka cluster. It is compatible with Kafka versions 0.9.x and later.
-   **[Kafka Producer V1](kafka-producer-v1-aecfaf2.md "The Kafka Producer operator allows applications to send records or messages to topics on
		a Kafka cluster. It is compatible with Kafka versions 0.8.x and later.")**  
The Kafka Producer operator allows applications to send records or messages to topics on a Kafka cluster. It is compatible with Kafka versions 0.8.x and later.
-   **[MQTT Consumer](mqtt-consumer-709a1b6.md "The MQTT Consumer operator subscribes to MQTT topics, consumes its messages, and outputs
		them.")**  
The MQTT Consumer operator subscribes to MQTT topics, consumes its messages, and outputs them.
-   **[MQTT Producer](mqtt-producer-c0ca754.md "The MQTT Producer operator receives MQTT messages from a port and publishes them in a
		topic.")**  
The MQTT Producer operator receives MQTT messages from a port and publishes them in a topic.
-   **[NATS Consumer](nats-consumer-d2a345d.md "The NATS Consumer operator consumes messages from NATS and forwards them to the output
		port.")**  
The NATS Consumer operator consumes messages from NATS and forwards them to the output port.
-   **[NATS Producer](nats-producer-e7fd7de.md "The NATS Producer operator receives a message from the input port and publishes it into
		NATS.")**  
The NATS Producer operator receives a message from the input port and publishes it into NATS.
-   **[OpenAPI Client](openapi-client-8a70738.md "The OpenAPI client operator is a convenient client that is suitable for invoking
		services described in a OpenAPI document. However, its use is not limited to those services
		described in OpenAPI documentation, and it can be used to invoke arbitrary REST
		services.")**  
The OpenAPI client operator is a convenient client that is suitable for invoking services described in a OpenAPI document. However, its use is not limited to those services described in OpenAPI documentation, and it can be used to invoke arbitrary REST services.
-   **[OpenAPI Server](openapi-server-1e23998.md "The OpenAPI server operator is a convenient server-side component that is suitable for providing services described in OpenAPI
		documentation or unspecified HTTP services. The component runs behind the web container of the hosting platform and inherits its security
		configuration. More concretely, this operator is configured to start its REST endpoint relative to the Pipeline engine's service path at
			/openapi/service/basePath/.")**  
The OpenAPI server operator is a convenient server-side component that is suitable for providing services described in OpenAPI documentation or unspecified HTTP services. The component runs behind the web container of the hosting platform and inherits its security configuration. More concretely, this operator is configured to start its REST endpoint relative to the Pipeline engine's service path at `/openapi/service/basePath/.`
-   **[SAP HANA Client](sap-hana-client-c25dff3.md "Executes SQL statements and inserts CSV or JSON data into an SAP HANA instance. It
		supports three fundamental operations:")**  
Executes SQL statements and inserts CSV or JSON data into an SAP HANA instance. It supports three fundamental operations:
-   **[SAP HANA Monitor](sap-hana-monitor-9de323a.md "This operator watches a HANA table and outputs newly inserted rows as a
		message.")**  
This operator watches a HANA table and outputs newly inserted rows as a message.
-   **[WAMP Consumer](wamp-consumer-de1740e.md "The WAMP Consumer operator is used to access records from Web Application Messaging
		Protocol (WAMP).")**  
The WAMP Consumer operator is used to access records from Web Application Messaging Protocol \(WAMP\).
-   **[WAMP Producer](wamp-producer-f6479fe.md "The WAMP Producer operator writes files to Web Application Messaging Protocol
		(WAMP).")**  
The WAMP Producer operator writes files to Web Application Messaging Protocol \(WAMP\).

