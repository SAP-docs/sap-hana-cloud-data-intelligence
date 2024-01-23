<!-- loiobbb754a8cffe470bac8b5ed9b3b3d219 -->

# Kafka to HANA

This scenario showcases how to read from a Kafka server topic and write the data into a HANA database table.



The [Kafka Consumer V2](../data-intelligence-operators/kafka-consumer-v2-6d4be10.md) reads data from a topic containing data formatted as JSON or CSV \(like in the HANA to Kafka graph\), where each message represents an entire row, and the [Binary to Table V2](../data-intelligence-operators/binary-to-table-v2-1bb16c0.md) converts the data into a Table format that is readable for the Write Table operator.

In case of failures, such as a network outage, the graph will fail, and upon restart, will recover from the last snapshot saved. As the Kafka Consumer commits the consumed messages on snapshot completion, it may resend them on restart, which is why the Write Table operator is configured to use UPSERT.

The graph runs indefinitely as the Kafka Consumer can continuously read from the topic and send it to the HANA side.



<a name="loiobbb754a8cffe470bac8b5ed9b3b3d219__section_ztf_mcp_pqb"/>

## Prerequisites

You need a running HANA database and a Kafka server to connect to.



<a name="loiobbb754a8cffe470bac8b5ed9b3b3d219__section_xx2_ncp_pqb"/>

## Configure and Run the Graph

Follow the steps below to run the example from the Data Pipeline UI:

1.  Select the 'Kafka to HANA' graph.

2.  Check the connection configuration of the three HANA and Kafka operators.

3.  Adjust the SOURCE Kafka topic and TARGET table specifications.




<a name="loiobbb754a8cffe470bac8b5ed9b3b3d219__section_qqv_31p_pqb"/>

## Operator Configuration

Aside from the standard configuration options of each operator, such as the connection information, the following configurations are necessary for the scenario to run with the new features enabled:

-   [Kafka Consumer V2](../data-intelligence-operators/kafka-consumer-v2-6d4be10.md)

    -   `Auto Commit`: *True*

-   [Initialize HANA Table V2](../data-intelligence-operators/initialize-hana-table-v2-5f52e92.md)

    -   `Configuration Mode`: *Static*
    -   `Initialization Mode`: *Create*


-   [Write HANA Table V2](../data-intelligence-operators/write-hana-table-v2-b6a5c17.md)
    -   `Configuration Mode`: *Static*
    -   `Statement Type`: *UPSERT*



