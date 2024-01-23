<!-- loioe69827d09d394db2be62ff396ea820d0 -->

# Flowagent SQL Consumer Graph

This graph demonstrates how to use Flowagent to perform a SQL query from a source and load it into a file.



This graph also shows how to read from the SQL query in parallel through the `logical partitioning` concept. To know more about logical partitioning specification, see the [Partitioning](../data-intelligence-operators/partitioning-86085d9.md) documentation.



### SQL Consumer

The SQL Consumer operator takes in a native SQL statement which will be pushdown to a MySQL database, and the response will be fetched in batches of N rows \(defined by **fetch size**\) and loaded to the next operator in line.



<a name="loioe69827d09d394db2be62ff396ea820d0__section_u2q_r5x_spb"/>

## Prerequisite

See MySQL driver configuration in the connection documentation present in the Connection Management.



<a name="loioe69827d09d394db2be62ff396ea820d0__section_bjk_v5x_spb"/>

## Components

-   **Reader definition**

    sqlconsumer1: Operator which performs the SQL query in a database.

    > ### Note:  
    > This operator should be configured before its usage.

-   **Loader definition**

    structuredfileproducer1: Operator that reads and writes the data into a file. Only cloud storages are supported.

-   **Wait to terminate graph**

    messageoperator1: Operator that waits for all partitions to finish before sending a message to graph terminator.


