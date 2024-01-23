<!-- loioec9764dc4b794419bfac18663d45b035 -->

# SAP CP EM Production Example

This graph demonstrates the publication of messages via SAP BTP Enterprise Messaging \(formerly SAP Cloud Platform Enterprise Messaging\).



<a name="loioec9764dc4b794419bfac18663d45b035__section_wws_fqs_1nb"/>

## Prerequisites

For this graph to run, you need:

-   A running instance of the SAP BTP Enterprise Messaging service.

-   A connection to this service instance configured in Connection Management.



<a name="loioec9764dc4b794419bfac18663d45b035__section_itp_js5_bgb"/>

## Configure and Run the Graph

1.  Open the configuration of the SAP CP EM Consumer operator and perform the following steps:
    1.  Select the connection to the SAP BTP Enterprise Messaging service instance for the *CP EM Connection* parameter.

    2.  Enter the topic to which you want to publish messages in the *Target Topic* parameter. The topic must conform to the namespace of the SAP BTP Enterprise Messaging service instance.
    3.  The remaining parameters are optional; if you don't specify them, a 0 value is used by default for each of them.

2.  Run the graph by clicking the *Run* button.
3.  Open the *Status Monitor* terminal to see any error messages that might occur during execution of the graph.
4.  Open the *Ack Monitor* terminal to see the number of acknowledged messages sent to the SAP BTP Enterprise Messaging service instance. If you are using the `maxCount` configuration parameter, you may need to disconnect the *Graph Terminator* operator to be able to open a terminal before the graph commpletes.

