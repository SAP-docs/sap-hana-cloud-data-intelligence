<!-- loio33c412a3d9114ba4960dc6678a15fce4 -->

# Data Extraction from SAP ABAP Table to Kafka via SLT

The Graph extracts data from an SAP ABAP table via SAP Landscape Transformation Replication Server \(SLT\) to a Kafka-Broker.



<a name="loio33c412a3d9114ba4960dc6678a15fce4__section_z1w_zh1_rqb"/>

## Prerequisites

1.  You need a valid connection to an ABAP System that runs an already configured SLT central server. Please create a valid and checked connection of type ABAP to an SAP S/4HANA environment or to an SAP NetWeaver/ABAP based system and do the basic SLT configuration in this system. A configuration of type `Data Intelligence` needs to be created upfront in SLT.

2.  You need a valid connection to a file store and the ability to create, read and write files to that file store location.




<a name="loio33c412a3d9114ba4960dc6678a15fce4__section_msk_n21_rqb"/>

## Configure the Snippet and Run the Graph

1.  Configure the [SLT Connector](../data-intelligence-operators/slt-connector-ac5b713.md) operator.

    1.  Choose a previously created `ABAP` connection to an SAP S/4 HANA onPremise or Cloud System.

    2.  Enter a unique subscription name for the data transfer. The subscription allows to resume a graph that was stopped or canceled at a later point in time. By default the snippet configuration will always result in creating a new subscription.

    3.  Enter the three digit `Mass Transfer ID` of the previously created SLT configuration.

    4.  Enter the name of an ABAP Table, for example `MARA`.

    5.  Enter the number of records that should be transferred in one batch to SAP Data Intelligence per roundtrip.

        > ### Note:  
        > Increasing this number has an impact on the memory consumption on the connected ABAP System and the Graph.

    6.  Choose the transfer mode. See the [SLT Connector](../data-intelligence-operators/slt-connector-ac5b713.md) operator documentation for more details.


2.  Configure the Kafka Producer operator according to the operator documentation.

3.  Create the graph from the snippet.

4.  Run the resulting graph by clicking the *Run* button.




<a name="loio33c412a3d9114ba4960dc6678a15fce4__section_dj1_qf1_rqb"/>

## Additional Remarks

1.  The graph will be always created with the setting for creating a new subscription.If an existing subscription should be used, it needs to be selected after the graph is created.

2.  Graph only stops automatically when `Initial Load` is chosen as transfer mode. In all other cases the graph will continue to run as `message.lastBatch` header is never sent, and therefore the graph is not getting terminated.


