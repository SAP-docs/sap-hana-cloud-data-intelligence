<!-- loiocd22a2cd6387487c9014fb19813dcd40 -->

# Data Extraction from SAP S4/HANA CDS View to KAFKA

Extracts data fom an ABAP CDS View to the KAFKA and creates related messages.



Not mandatory, but for convenience, this example re-reads the data from the KAFKA feed and redirects it to the Terminal operator.



<a name="loiocd22a2cd6387487c9014fb19813dcd40__section_zmq_1vc_1kb"/>

## Prerequisites

-   You need a valid connection to SAP S/4HANA. Please create a valid and checked connection to an SAP S/4HANA environment or to an SAP NetWeaver/ABAP based system that supports the CDS technology. Please use the related description of the SAP DI - Connection Management to implement and test such a connection. In this example the communication is based on HTTPS, but you may use other protocols such as HTTP, RFC or \(WebSocket\) WSRFC

-   You need a checked KAFKA connection and the ability to create, read and write messages to KAFKA. Please use the related description of the SAP DI - Connection Management to implement and test such a connection.

-   A couple of Operators need to be in place:

    -   [ABAP CDS Reader](../data-intelligence-operators/abap-cds-reader-df331fc.md)

    -   [ABAP Converter](../data-intelligence-operators/abap-converter-d58c19e.md)

    -   [Go Operator](../data-intelligence-operators/go-operator-aabb1ca.md)

    -   [Graph Terminator](../data-intelligence-operators/graph-terminator-26f7ff3.md)

    -   [Kafka Producer V1](../data-intelligence-operators/kafka-producer-v1-aecfaf2.md)

    -   [Kafka Consumer V1](../data-intelligence-operators/kafka-consumer-v1-582b188.md)

    -   [Terminal](../data-intelligence-operators/terminal-2f28daf.md)

    -   [Wiretap](../data-intelligence-operators/wiretap-2a0c233.md)


-   The CDS View must allow data extraction via the annotation: `@Analytics:{ dataExtraction: enabled: true ...` for delta extraction. The `delta.changeDataCapture` part of the annotation needs to be maintained correctly.




<a name="loiocd22a2cd6387487c9014fb19813dcd40__section_ebl_jvc_1kb"/>

## Configure and Run the Graph

1.  In this example the ABAP CDS Reader is configured to execute an initial load.

    The CDS Reader supports 3 ways to load data:

    -   The straight forward Initial Load, which copies the data from source to target but without any subsequent replication;

    -   The Replication, which includes the Initial Load and - based on a delta handling - the subsequent replication of changed data;

    -   The Delta Processing, which implies that no Initial Load takes place and changed data only will get processed.


2.  The ABAP Converter feeds via a Message Converter into a Go Operator `Determine Last Batch`, which checks whether the SLT-based replication got stopped and is then launching a soft-kill \(used at `Check Last Batch`\)

    The data keep flowing into KAFKA Producer using topic `test_topic`.

    The KAFKA Producer converts the records to messages within the configured parameters to KAFKA Topic `test_topic`.

    The Go Operator `Check Last Batch` terminates the graph in case of the end of the replication; without the two operators `* Last Batch`, it can happen that the graph gets terminated before the last write got completed.

    Optional: simply to visualize the flow, the just used and created messages can be consumed by a KAFKA consumer and sent to Terminal/Wiretap.

    Use to execute this Graph.




<a name="loiocd22a2cd6387487c9014fb19813dcd40__section_xhm_byc_1kb"/>

## Data Integration and Data Security

Please make yourself familiar with the related Integration Guides and Security considerations such as [User Guide for ABAP Integration in SAP Data Intelligence](https://help.sap.com/viewer/3a65df0ce7cd40d3a61225b7d3c86703/Cloud/en-US/8b287f0f0033447c8a57a1bee74cd840.html "This guide is relevant for you if your use case for SAP Data Intelligence Cloud involves ABAP-based SAP systems, such as SAP S/4HANA or SAP Business Warehouse (BW).") :arrow_upper_right:, the [Administration Guide for SAP Data Intelligence](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/884ffcd587784ed2a311b2c19feb8410.html "The SAP Data Intelligence Administration Guide contains information about configuring, monitoring, and managing SAP Data Intelligence.") :arrow_upper_right:, and SAP Note [2831756](https://me.sap.com/notes/2831756) .

