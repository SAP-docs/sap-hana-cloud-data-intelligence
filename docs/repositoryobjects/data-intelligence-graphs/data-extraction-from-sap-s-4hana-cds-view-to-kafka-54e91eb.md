<!-- loio54e91ebb236840beb7e3a9d0723924f4 -->

# Data Extraction from SAP S/4HANA CDS View to Kafka

The Graph extracts data from an ABAP CDS View to a Kafka-Broker.



<a name="loio54e91ebb236840beb7e3a9d0723924f4__section_sws_3g1_rqb"/>

## Prerequisites

1.  You need a valid connection to SAP S/4HANA. Please create a valid and checked connection of type ABAP to an SAP S/4HANA environment or to an SAP NetWeaver/ABAP based system which supports the CDS technology.

2.  The CDS View must allow data extraction via the annotation: “@Analytics:\{ dataExtraction: enabled: true …” - for delta extraction also the “delta.changeDataCapture” part of the annotation needs to be maintained correctly.

3.  You need a valid connection to a file store and the ability to create, read and write files to that file store location.




<a name="loio54e91ebb236840beb7e3a9d0723924f4__section_msk_n21_rqb"/>

## Configure the Snippet and Run the Graph

1.  Configure the [ABAP CDS Reader](../data-intelligence-operators/abap-cds-reader-df331fc.md) operator.

    1.  Choose a previously created `ABAP` connection to an SAP S/4 HANA onPremise or Cloud System.

    2.  Enter a unique subscription name for the data transfer. The subscription allows to resume a graph that was stopped or canceled at a later point in time. By default the snippet configuration will always result in creating a new subscription.

    3.  Enter the name of an extraction enabled ABAP CDS View, for example `I_BUSINESSPARTNER`.

    4.  Choose the transfer mode. See the [ABAP CDS Reader](../data-intelligence-operators/abap-cds-reader-df331fc.md) operator documentation for more details.

    5.  Enter the number of records that should be transferred in one batch to SAP Data Intelligence per roundtrip.

        > ### Note:  
        > Increasing this number has an impact on the memory consumption on the connected ABAP System and the Graph.


2.  Configure the Kafka Producer operator according to the operator documentation.

3.  Create the graph from the snippet.

4.  Run the resulting graph by clicking the *Run* button.




<a name="loio54e91ebb236840beb7e3a9d0723924f4__section_dj1_qf1_rqb"/>

## Additional Remarks

1.  The graph will be always created with the setting for creating a new subscription.If an existing subscription should be used, it needs to be selected after the graph is created.

2.  Graph only stops automatically when `Initial Load` is chosen as transfer mode. In all other cases the graph will continue to run as `message.lastBatch` header is never sent, and therefore the graph is not getting terminated.


