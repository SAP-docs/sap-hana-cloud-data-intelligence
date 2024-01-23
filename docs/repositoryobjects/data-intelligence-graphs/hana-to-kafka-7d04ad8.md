<!-- loio7d04ad88788f465d9213d920319bc3e9 -->

# HANA to Kafka

This scenario showcases how to read a HANA database table and write the data into a Kafka server.



The [Read HANA Table V2](../data-intelligence-operators/read-hana-table-v2-b51aded.md) copies data from a table based on the [Load into SAP HANA](load-into-sap-hana-d57498a.md) scenario, and the [Table to Binary](../data-intelligence-operators/table-to-binary-f0ba7fa.md) converts the table data into JSON/CSV format, so it can be finally consumed by the [Kafka Producer V2](../data-intelligence-operators/kafka-producer-v2-e22d0e5.md).

In case of failures, such as a network outage, the graph will fail, and upon restart, will recover from the last snapshot saved, avoiding the need of reading the whole table again.

The table data is sent in batches by the HANA operator, with each message being streamed from one operator to another. Since the Kafka Producer deals with binary data, each batch has to be of size 1. For that reason, the start and end of each row can be identified.



<a name="loio7d04ad88788f465d9213d920319bc3e9__section_ztf_mcp_pqb"/>

## Prerequisites

You need a running HANA database and a Kafka server to connect to.



<a name="loio7d04ad88788f465d9213d920319bc3e9__section_xx2_ncp_pqb"/>

## Configure and Run the Graph

Follow the steps below to run the example from the Data Pipeline UI:

1.  Select the 'HANA to Kafka' graph.

2.  Check the connection configuration of the three HANA and Kafka operators.

3.  Adjust the SOURCE table name and TARGET Kafka topic.




<a name="loio7d04ad88788f465d9213d920319bc3e9__section_qqv_31p_pqb"/>

## Operator Configuration

Aside from the standard configuration options of each operator, such as the connection information, the following configurations are necessary for the scenario to run with the new features enabled:

-   [Read HANA Table V2](../data-intelligence-operators/read-hana-table-v2-b51aded.md)

    -   `Configuration Mode`: *Static*
    -   `Batching`: *Fixed size*

    -   `Batch Size(row)`: *1*

-   [Kafka Producer V2](../data-intelligence-operators/kafka-producer-v2-e22d0e5.md)
    -   `Async Mode`: *True*



