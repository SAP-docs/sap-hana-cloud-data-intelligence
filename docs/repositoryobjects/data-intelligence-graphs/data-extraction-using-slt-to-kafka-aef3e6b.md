<!-- loioaef3e6be31204adf8f8fd7d69adcc8a5 -->

# Data Extraction using SLT to KAFKA

Extracts data fom an ABAP table using SLT to the KAFKA and creates related messages.



Not mandatory, but for convenience, this example re-reads the data from the KAFKA feed and redirects it to the Terminal operator.



<a name="loioaef3e6be31204adf8f8fd7d69adcc8a5__section_zmq_1vc_1kb"/>

## Prerequisites

-   You need a valid connection to the SAP LT Replication Server / SLT. Please create a valid and checked connection to an the SAP LT Replication Server / SLT system that supports the necessary SLT scenarios. Please use the related description of the SAP DI - Connection Management to implement and test such a connection. In this example the communication is based on HTTPS, but you may use other protocols such as HTTP, RFC or \(WebSocket\) WSRFC.

-   You need a checked KAFKA connection and the ability to create, read and write messages to KAFKA. Please use the related description of the SAP DI - Connection Management to implement and test such a connection. In this example we used KAFKA as the consumer of the created messages.

-   A couple of Operators need to be in place: \(ABAP\) SLT Connector, ABAP Converter, Go Operator \( → String Operator, Determine Last Batch, Limit File Size, Check Last Batch\), Python \( → splitting a portion of records to single records for messaging\), Graph Terminator, KAFKA Producer and Consumer, Terminal, Wiretap.




<a name="loioaef3e6be31204adf8f8fd7d69adcc8a5__section_og5_sb2_1kb"/>

## Configure and Run

1.  In this example the SLT Connector replicates the specified ABAP table to KAFKA. The CDS Reader supports 3 ways to load data: a\) the straight forward Initial Load, which copies the data from source to target but without any subsequent replication. b\) the Replication, which includes the Initial Load and - based on a delta handling - the subsequent replication of changed data. c\) the Delta Processing, which implies that no Initial Load takes place and changed data only will get processed.

2.  The ABAP Converter feeds via a Message Converter into a Go operator `Determine Last Batch`, which checks whether the SLT-based replication got stopped and is then launching a soft-kill \(used at `Check Last Batch`\)

3.  The data keep flowing into KAFKA Producer using topic `test_topic_SLT`.

4.  The KAFKA Producer converts the records to messages within the configured parameters to KAFKA Topic `test_topic_SLT`.

5.  The Go Operator `Check Last Batch` terminates the graph in case of the end of the replication; without the two operators `* Last Batch`, it can happen that the graph gets terminate before the last write got completed.

6.  \(optional\) To simply visualize the flow, the just used and created messages can be consumed by a KAFKA consumer and sent to Terminal/Wiretap.

7.  Use to execute this Graph.


> ### Note:  
> To improve performance: implementation of a Phyton script that splits the portion based table extraction into individual line items to support a single-message-based-on-single-data-record messaging.



<a name="loioaef3e6be31204adf8f8fd7d69adcc8a5__section_xhm_byc_1kb"/>

## Data Integration and Data Security

Please make yourself familiar with the related Integration Guides and Security considerations such as [User Guide for ABAP Integration in SAP Data Intelligence](https://help.sap.com/viewer/3a65df0ce7cd40d3a61225b7d3c86703/Cloud/en-US/8b287f0f0033447c8a57a1bee74cd840.html "This guide is relevant for you if your use case for SAP Data Intelligence Cloud involves ABAP-based SAP systems, such as SAP S/4HANA or SAP Business Warehouse (BW).") :arrow_upper_right:, the [Administration Guide for SAP Data Intelligence](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/884ffcd587784ed2a311b2c19feb8410.html "The SAP Data Intelligence Administration Guide contains information about configuring, monitoring, and managing SAP Data Intelligence.") :arrow_upper_right:, and SAP Note [2831756](https://me.sap.com/notes/2831756) .

