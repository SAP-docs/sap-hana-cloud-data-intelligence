<!-- loio47178dd574d74579ad91eaa32ce96025 -->

# HANA to HANA

This scenario showcases how to read one HANA database table and write to another.



The [Read HANA Table V2](../data-intelligence-operators/read-hana-table-v2-b51aded.md) copies data from a table based on the [Load into SAP HANA](load-into-sap-hana-d57498a.md) scenario.

[Initialize HANA Table V2](../data-intelligence-operators/initialize-hana-table-v2-5f52e92.md) creates or initializes a new table based on its configurations.

[Write HANA Table V2](../data-intelligence-operators/write-hana-table-v2-b6a5c17.md) performs UPSERTs on the target table based on the inputs that are forwarded from Read\>Init\>Write.

In case of failures, such as a network outage, the graph will fail and upon restart will recover from the last snapshot saved, avoiding the need to read the whole table again.

The table data is sent in batches by the HANA operator, with each message being streamed from one operator to another. The batch information available in the message headers are used by the [Graph Terminator V2](../data-intelligence-operators/graph-terminator-v2-190cbc7.md) operator to determine when the operation is complete.



<a name="loio47178dd574d74579ad91eaa32ce96025__section_ztf_mcp_pqb"/>

## Prerequisites

You need a running HANA database to connect to.



<a name="loio47178dd574d74579ad91eaa32ce96025__section_xx2_ncp_pqb"/>

## Configure and Run the Graph

Follow the steps below to run the example from the Data Pipeline UI:

1.  Select the 'HANA to HANA' graph.

2.  Check the connection configuration of the three HANA operators.

3.  Adjust the SOURCE and TARGET table names.

4.  Adjust the TARGET Column entries in the [Initialize HANA Table V2](../data-intelligence-operators/initialize-hana-table-v2-5f52e92.md) operator, to ensure that they match some or all SOURCE table columns.

5.  Ensure that the TARGET table contains at least one primary key column for the UPSERT to work.




<a name="loio47178dd574d74579ad91eaa32ce96025__section_lgm_2dp_pqb"/>

## Operator Configuration

Aside from the standard configuration options of each operator, such as the connections to the database and file system, the following configurations are necessary for the scenario to run with the new features enabled:

-   [Read HANA Table V2](../data-intelligence-operators/read-hana-table-v2-b51aded.md)

    -   `Configuration Mode`: *Static*

    -   `Batching`: *Fixed size*


-   [Initialize HANA Table V2](../data-intelligence-operators/initialize-hana-table-v2-5f52e92.md)
    -   `Configuration Mode`: *Static*

    -   `Output Initialized Table`: *False*


-   [Write HANA Table V2](../data-intelligence-operators/write-hana-table-v2-b6a5c17.md)
    -   `Configuration Mode`: *Static*

    -   `Statement Type`: *UPSERT*


-   [Graph Terminator V2](../data-intelligence-operators/graph-terminator-v2-190cbc7.md)
    -   `On Last Batch`: *True*



