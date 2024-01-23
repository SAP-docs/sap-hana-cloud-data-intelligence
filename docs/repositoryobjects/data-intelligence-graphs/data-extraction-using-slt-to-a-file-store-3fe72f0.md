<!-- loio3fe72f0cde894aa6a19ea4d910be6aae -->

# Data Extraction using SLT to a File Store

Extracts data fom an ABAP table using SLT to a file store and creates related files in the file store.



In this example, the source is an SAP S/4HANA. Not mandatory, but for convenience, this example may be extended to read the data from the written files and to feed into the Terminal operator.



<a name="loio3fe72f0cde894aa6a19ea4d910be6aae__section_zmq_1vc_1kb"/>

## Prerequisites

-   You need a valid connection to the SAP S/4HANA source. Please create a valid and checked connection to an SAP S/4HANA environment or to an SAP NetWeaver/ABAP based system that supports the SLT technology. Please use the related description of the SAP DI - Connection Management to implement and test such a connection. In this example the communication is based on HTTPS, but you may use other protocols such as HTTP, RFC or \(WebSocket\) WSRFC.

-   You need a valid connection to a file store and the ability to create, read and write files to that file store location. Please use the related description of the SAP DI - Connection Management to implement and test such a connection. In this example we used S3 as a target file store.

-   A couple of operators need to be in place:

    -   [SLT Connector](../data-intelligence-operators/slt-connector-ac5b713.md)
    -   [ABAP Converter](../data-intelligence-operators/abap-converter-d58c19e.md)

    -   [Go Operator](../data-intelligence-operators/go-operator-aabb1ca.md) \(→ Determine Last Batch, Limit File Size, Check Last Batch\)

    -   [Read File \(Deprecated\)](../data-intelligence-operators/read-file-deprecated-df00daf.md)

    -   [Write File \(Deprecated\)](../data-intelligence-operators/write-file-deprecated-43e1cc8.md)

    -   [Graph Terminator](../data-intelligence-operators/graph-terminator-26f7ff3.md)





<a name="loio3fe72f0cde894aa6a19ea4d910be6aae__section_og5_sb2_1kb"/>

## Configure and Run

1.  In this example the SLT Connector replicates the an ABAP table to S3.

2.  The ABAP Converter feeds via a Message Converter into a Go Operator `Determine Last Batch`, which checks whether the SLT-based replication got stopped and is then launching a soft-kill \(used at `Check Last Batch`\)

3.  The data keep flowing into a Go operator `Limit File Size`, which controls the file size as a parameter and the file counter.

4.  The Write File operator is used to create the files until end-of-initial-load. The Write File operator uses the configured 'append' mode to fill into`/tmp/file_${ABAPfilenumber}.csv` as of Service `S3` and its configured connection.

5.  The Go operator `Check Last Batch` terminates the graph in case of the end of the replication; without the two operators `* Last Batch`, it can happen that the graph gets terminated before the last write got completed.

6.  \(optional\) To simply visualize the file, the just used and created file on S3 may be read again and sent to Terminal.

7.  Use to execute this Graph.

    > ### Note:  
    > In case of an Initial Load only, the graph will terminate, in case of Delta Mode or Replication \(`=Initial Load plus Delta`\) the graph will not stop after the initial load.




<a name="loio3fe72f0cde894aa6a19ea4d910be6aae__section_xhm_byc_1kb"/>

## Data Integration and Data Security

Please make yourself familiar with the related Integration Guides and Security considerations such as [User Guide for ABAP Integration in SAP Data Intelligence](https://help.sap.com/viewer/3a65df0ce7cd40d3a61225b7d3c86703/Cloud/en-US/8b287f0f0033447c8a57a1bee74cd840.html "This guide is relevant for you if your use case for SAP Data Intelligence Cloud involves ABAP-based SAP systems, such as SAP S/4HANA or SAP Business Warehouse (BW).") :arrow_upper_right:, the [Administration Guide for SAP Data Intelligence](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/884ffcd587784ed2a311b2c19feb8410.html "The SAP Data Intelligence Administration Guide contains information about configuring, monitoring, and managing SAP Data Intelligence.") :arrow_upper_right:, and SAP Note [2831756](https://me.sap.com/notes/2831756) .

