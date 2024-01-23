<!-- loio789a630cfa0f453aaef20c560e19e785 -->

# SAP CP EM Consumption Example

This graph demonstrates the consumption of messages from SAP BTP Enterprise Messaging.



<a name="loio789a630cfa0f453aaef20c560e19e785__section_wws_fqs_1nb"/>

## Prerequisites

For this graph to run, you need the following:

-   A running instance of the SAP BTP enterprise messaging service.

-   A connection to this service instance configured in Connection Management.



<a name="loio789a630cfa0f453aaef20c560e19e785__section_itp_js5_bgb"/>

## Configure and Run the Graph

1.  Open the configuration of the SAP CP EM Consumer operator and perform the following steps:
    1.  Select the connection to the SAP BTP enterprise messaging service instance for the *CP EM Connection* parameter.

    2.  Enter the queue from which you want to retrieve messages in the *Source Queue* parameter. The queue must exist on the SAP BTP enterprise messaging service instance.
    3.  The remaining parameters are optional; if you don't specify them, a 0 value is used by default for each of them.

2.  Run the graph by clicking the *Run* button.
3.  Open the *Status Monitor* terminal to see any error messages that may occur during execution of the graph.
4.  Open the *Payload Monitor* terminal to see the messages received from the SAP BTP enterprise messaging service instance. If you are using the `maxCount` configuration parameter, you may need to disconnect the *Graph Terminator* operator to be able to open a terminal before the graph completes.

