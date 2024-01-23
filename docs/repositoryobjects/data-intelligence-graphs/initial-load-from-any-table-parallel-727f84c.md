<!-- loio727f84c0eeba40a2a0ae4998ee94a081 -->

# Initial Load from any Table \(parallel\)

Demonstrates how to read contents from any table and load it into a file.



In this graph, a Table Consumer is used to read a table, which is configured and then its content is converted into CSV and written into a file by the Structured File Producer operator.

This graph also shows how to read from the table in parallel through the logical partitioning concept. For more information, see [Logical Partitions](../data-intelligence-operators/logical-partitions-83ccb1c.md).



<a name="loio727f84c0eeba40a2a0ae4998ee94a081__section_zmq_1vc_1kb"/>

## Prerequisites

To run this graph:

1.  Create a connection supported by the Table Consumer operator in Connection Management. For more information about the connections supported, see [Table Consumer V2](../data-intelligence-operators/table-consumer-v2-1e5f0ee.md). Also check the connection type documentation in the Connection Management application.
2.  Open the custom UI, and select the Service, Connection ID, and Source.
3.  In the operator Configuration panel, configure the Logical Partition Specification, defining the partitions to be read in parallel.



<a name="loio727f84c0eeba40a2a0ae4998ee94a081__section_og5_sb2_1kb"/>

## Components



### Reader definition

tableconsumer1: operator that reads from the Oracle table.



### Loader definition

structuredfileproducer1: operator that reads and writes the data into a file. Local and cloud storages are both supported.



### Wait to terminate graph

messageoperator1: operator that waits for all partitions to finish before sending a message to graph terminator.



### Configuration Substitutions

NUM\_PARALLEL\_EXECUTORS: Specify the number of logical partitions.

**Related Information**  


[Logical Partitions](../data-intelligence-operators/logical-partitions-83ccb1c.md "Logical partitions are user-defined chunks of data, where each chunk contains a filter that specifies the chunk of data to be read.")

