<!-- loio771105b487c64787a0aa6aebd38e8624 -->

# Connecting to Kafka in Streaming Analytics Project CCL

This example graph shows how a streaming analytics project can use adapters to consume data from a Kafka topic that is produced using a Kafka Producer operator. It also shows how to publish to a Kafka topic that is then consumed using a Kafka Consumer operator. The Kafka Input and Output adapters are added to the streaming analytics operator using Continuous Computation Language \(CCL\).



## Prerequisites

-   In the project CCL, set the kafkaBootstrapServers property on the Kafka CSV Input and Output adapters to point to your Kafka broker\(s\). Do the same with the Brokers property on the Kafka Producer and Consumer operators.

-   Create a new Dockerfile that inherits the streaming analytics one \(`FROM $com.sap.sles.streaming`\).

-   Add an additional tag to the Dockerfile that can be used to identify your CCL project.

-   Upload the Kafka client jar to `/files/vflow/dockerfiles/<path-to-new-dockerfile>/` using the System Management Files application. Only the Kafka 0.9.x and 0.10.x versions are supported.

-   Update the new Dockerfile to copy the Kafka client jar to `$STREAMING_HOME/adapters/framework/libj` folder. The streaming Dockerfile currently includes an example of that.

-   Copy this example graph, and move all operators inside a group that uses the new tag \(see [Docker Inheritance documentation](https://help.sap.com/docs/SAP_DATA_INTELLIGENCE/1c1341f6911f4da5a35b191b40b426c8/d49a07c5d66c413ab14731adcfc4f6dd.html?locale=en-US) for more information\).


**Related Information**  


[Setting Up the Kafka Adapters](https://help.sap.com/viewer/52acc1f6b1d7428caab280d193c820f6/latest/en-US/0d987463c09445b7a48c1b84e13ab31e.html)

