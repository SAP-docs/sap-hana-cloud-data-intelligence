<!-- loio94ab34dfddfa4a298f91ec4cea4e56ba -->

# Google Pub/Sub

This example shows how to publish messages using the Google Pub/Sub Producer, and consume them via the Google Pub/Sub Consumer.



<a name="loio94ab34dfddfa4a298f91ec4cea4e56ba__section_obf_gsf_dfb"/>

## Prerequisites

-   A project on GCP with access to the Pub/Sub service and the corresponding access key file as JSON.



<a name="loio94ab34dfddfa4a298f91ec4cea4e56ba__section_lmw_t4f_dfb"/>

## Configure and Run the Graph

Follow the steps below to run the example from the SAP Data Intelligence Modeler UI:

1.  In the left panel, select the *Graphs* tab and open the Google Pub/Sub graph.
2.  Check the configuration of the *Google Pub/Sub Producer* operator.
3.  Create a connection containing a valid GCP project ID and corresponding key file using the manual configuration type. Alternatively, you can reuse an existing connection by selecting configuration manager as configuration type. Enter the name of the topic that the producer publishes to.
4.  Check the configuration of the "Google Pub/Sub consumer" node. Similar to the producer, consumer also requires a valid connection. Next, enter the subscription name and if this subscription does not exist on the Pub/Sub service, enter the same topic name as in the producer.
5.  In the tool bar, select *Run* \(play button\).
6.  The *Status* panel indicates if the graph is running.
7.  Use the context menu *Open UI* of the *publish/output* node to open the terminal. Here, any message you type in, is sent as a publication to the configured topic in the Google Pub/Sub service.
8.  The bottom half shows the output and error messages of the consumer and producer.
9.  Using the provided message ID, you can acknowledge receiving the message to the Google Pub/Sub service.
10. Open the context menu *Open UI* of the *ack/output* node to open the terminal.
11. Enter a message with the attribute: `{"msg.MessageID":"<MESSAGE_ID>"}` with `<MESSAGE_ID>` replaced with the message ID of the message to be acknowledged. If you do not explicitly acknowledge the message, after stopping the graph and restarting it, the message will be delivered again. In this case, the redelivered messages can be seen in the `Wiretap` node. Alternatively, you can disable explicit acknowledgment by removing the input connection to the `messageToAck` port of the `Google Pub/Sub Consumer`. In this case, any message received by the consumer is acknowledged automatically.

