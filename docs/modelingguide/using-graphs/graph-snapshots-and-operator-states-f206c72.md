<!-- loiof206c726e6d447f5b4df22a2d5ffe7b1 -->

# Graph Snapshots and Operator States

You can configure Generation 2 \(Gen2\) graphs to take snapshots of their state at regular time intervals so that the operators of the graph send small pieces of data \(status\) to a central data store.

If the graph fails or pauses, SAP Data Intelligence Modeler uses the last status data to reinitialize to the last state before the failure or pause happened.

> ### Example:  
> If a graph is processing a large database table, its operator regularly saves which rows it has already processed. When recovering from a failure, the operator reads its last used state and continues processing from the specific row instead of starting over from the beginning of the table.

If you also enable the snapshot feature, recovery of stateful graphs is more efficient than running with recovery only. Enable snapshots only when the Gen2 graph is conceptually stateful. If a graph doesn't have any state to save, it's more efficient to not capture snapshots.



<a name="loiof206c726e6d447f5b4df22a2d5ffe7b1__section_h2f_5mv_tvb"/>

## Keeping State Size Small

To keep the status data per operator small, design a computation method that incrementally maintains a small state size. Ensure that you design a computation method when you design the operator and before you implement the operator.

> ### Note:  
> The size of the stored state depends on the stateful computation by the operator, and not by the snapshot frequency.

> ### Example:  
> Calculate the total sales by city and send sales records to the operator in the graph through its input port, and manage the state size. There are two methods to achieve this goal.
> 
> **Method 1**
> 
> 1.  Group all records received by each city.
> 2.  After the last record is received, compute the sum of sales in each city group.
> 3.  Return the result.
> 
> For Method 1, the size of the state is roughly the size of all records received by the operator, no matter the snapshot frequency.
> 
> **Method 2**
> 
> Design an incremental version of the Method 1 computation:
> 
> 1.  Maintain a state where, for each city, you compute the current sum of sales amount.
> 2.  After all records are received, the state contains the result that is returned.
> 
> For Method 2, the size of the state is roughly the number of cities with their sum, independent of the snapshot frequency.



<a name="loiof206c726e6d447f5b4df22a2d5ffe7b1__section_avm_3hd_3xb"/>

## Operators That Support Snapshots

Not every Gen2 operator supports the snapshot feature. When you configure and run a Gen2 graph, but some of the operators in the graph don't support the snapshot feature, the graph can't reinitialize to the state before a failure or a pause, and it can lose data. Therefore, ensure that a graph that you run with the *Capture Snapshots* option enabled contains only operators that support snapshots.

The following table lists all Gen2 operators, whether they support snapshots, and any conditions that apply.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Operator

</th>
<th valign="top">

Operator ID

</th>
<th valign="top">

Supports Snapshots

</th>
<th valign="top">

Conditions and Remarks

</th>
</tr>
<tr>
<td valign="top">

ABAP

</td>
<td valign="top">

Read Data From SAP System

</td>
<td valign="top">

com.sap.abap.reader

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Stores state: list of package IDs in process.

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Kafka Consumer

</td>
<td valign="top">

com.sap.kafka.consumer2.v2

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

For details about conditions, see the section Snapshot Support in [Kafka Consumer V2](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/6d4be1097f8d4df0b18e3a606ae9b607.html "The Kafka Consumer operator works as a Kafka client that consumes records or messages from a Kafka cluster. It is compatible with Kafka versions 0.9.x and later.") :arrow_upper_right:.

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

Kafka Producer

</td>
<td valign="top">

com.sap.kafka.producer.v2

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

For details about conditions, see the section Snapshot Support in [Kafka Producer V2](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/e22d0e5f8f564a76a1fe0486845b0303.html "The Kafka Producer operator allows applications to send records or messages to topics on a Kafka cluster. It is compatible with Kafka versions 0.8.x and later.") :arrow_upper_right:.

</td>
</tr>
<tr>
<td valign="top">

Connectivity

</td>
<td valign="top">

REST API Client

</td>
<td valign="top">

com.sap.restapi.client

</td>
<td valign="top">

Yes

</td>
<td valign="top">

For details about conditions, see the section Snapshot Support in [Rest API Client](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/36aa260d17f54d738071b9c7a716faea.html "The Rest API Client operator performs HTTP requests according to its configurations and provided inputs.") :arrow_upper_right:.

</td>
</tr>
<tr>
<td valign="top">

Connectivity \(via Flowagent\)

</td>
<td valign="top">

Flowagent SQL Executor

</td>
<td valign="top">

com.sap.dh.ds.sql.executor.v2

</td>
<td valign="top">

No

</td>
<td valign="top">

None

</td>
</tr>
<tr>
<td valign="top">

Data Quality

</td>
<td valign="top">

Validation Rule

</td>
<td valign="top">

com.sap.dh.dq.validationrule.v2

</td>
<td valign="top">

No

</td>
<td valign="top">

None

</td>
</tr>
<tr>
<td valign="top">

Files

</td>
<td valign="top">

Binary File Consumer

</td>
<td valign="top">

com.sap.file.read.v2

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Stores state: index of the part file last read.

For details about conditions, see the section Snapshot Support in [Binary File Consumer](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/1faddfa3f3e14bcb98049e90ece74f1f.html "The Binary File Consumer operator reads the content of files from various storage services.") :arrow_upper_right:.

</td>
</tr>
<tr>
<td valign="top">

Files

</td>
<td valign="top">

Binary File Producer

</td>
<td valign="top">

com.sap.file.write.v2

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Stores state: See the section State Management Support in [Binary File Producer](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/64d01ad02e39499594b1eb103974443e.html "The Binary File Producer operator writes files to various services.") :arrow_upper_right:.

</td>
</tr>
<tr>
<td valign="top">

Files

</td>
<td valign="top">

List Files

</td>
<td valign="top">

com.sap.file.list.v2

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Stores state: index of file in the files list.

For details about conditions, see the section Snapshot Support in [List Files V2](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/4d4da2140f354ba09fa4a280527f6e07.html "The List Files operator lists files and directories from various storage services.") :arrow_upper_right:.

</td>
</tr>
<tr>
<td valign="top">

Processing

</td>
<td valign="top">

Python3 Operator

</td>
<td valign="top">

com.sap.system.python3Operator.v2

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Stores state: depends on user script.

</td>
</tr>
<tr>
<td valign="top">

Remote Dataflow

</td>
<td valign="top">

Data Services Transform

</td>
<td valign="top">

com.sap.dataservices.transform.v2

</td>
<td valign="top">

No

</td>
<td valign="top">

None

</td>
</tr>
<tr>
<td valign="top">

SAP HANA

</td>
<td valign="top">

Initialize HANA Table

</td>
<td valign="top">

com.sap.hana.initTable.v2

</td>
<td valign="top">

Yes

</td>
<td valign="top">

None

</td>
</tr>
<tr>
<td valign="top">

SAP HANA

</td>
<td valign="top">

Read HANA Table

</td>
<td valign="top">

com.sap.hana.readTable.v2

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Stores state: row index.

For details about conditions, see the section State Management Support in [Read HANA Table V2](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/b51adedc86404c79afda7bbca3b958aa.html "The Read HANA Table operator reads data from a table in SAP HANA.") :arrow_upper_right:.

</td>
</tr>
<tr>
<td valign="top">

SAP HANA

</td>
<td valign="top">

Run HANA SQL

</td>
<td valign="top">

com.sap.hana.runSQL.v2

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Stores state: last statement executed and the batch index.

For details about conditions, see the section State Management Support in [Run HANA SQL V2](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/5796f97071ac44b386172f686fdaf015.html "The Run HANA SQL operator executes user-provided SQL statements on an SAP HANA database.") :arrow_upper_right:.

</td>
</tr>
<tr>
<td valign="top">

SAP HANA

</td>
<td valign="top">

Write HANA Table

</td>
<td valign="top">

com.sap.hana.writeTable.v2

</td>
<td valign="top">

Yes

</td>
<td valign="top">

None

</td>
</tr>
<tr>
<td valign="top">

Structured Data Operators

</td>
<td valign="top">

SAP Application Consumer

</td>
<td valign="top">

com.sap.application.consumer.v3

</td>
<td valign="top">

No

</td>
<td valign="top">

None

</td>
</tr>
<tr>
<td valign="top">

Structured Data Operators

</td>
<td valign="top">

SAP Application Producer

</td>
<td valign="top">

com.sap.application.producer.v2

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Operator supports running with snapshots only when you use it with Structured Data Consumer operators with source partitions. However, the operator doesn't support snapshots when you use it with other consumer operators, like ABAP Readers.

</td>
</tr>
<tr>
<td valign="top">

Structured Data Operators

</td>
<td valign="top">

SQL Consumer

</td>
<td valign="top">

com.sap.database.sql.consumer.v3

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Stores state: partition of input data.

Operator supports running with snapshots only when it reads data using partitions, and when you use it with Structured Data Producer operators.

</td>
</tr>
<tr>
<td valign="top">

Structured Data Operators

</td>
<td valign="top">

Table Consumer

</td>
<td valign="top">

com.sap.database.table.consumer.v3

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Stores state: partition of database table.

Operator supports running with snapshots only when it reads data using partitions, and when you use it with Structured Data Producer operators.

</td>
</tr>
<tr>
<td valign="top">

Structured Data Operators

</td>
<td valign="top">

Table Producer

</td>
<td valign="top">

com.sap.database.table.producer.v4

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Operator supports running with snapshots only when you use it with Structured Data Consumer operators with source partitions. However, the operator doesn't support snapshots when you use it with other consumer operators, like ABAP Readers.

</td>
</tr>
<tr>
<td valign="top">

Structured Data Operators

</td>
<td valign="top">

Data Transform

</td>
<td valign="top">

com.sap.datatransform.v2

</td>
<td valign="top">

No

</td>
<td valign="top">

None

</td>
</tr>
<tr>
<td valign="top">

Structured Data Operators

</td>
<td valign="top">

Structured File Consumer

</td>
<td valign="top">

com.sap.storage.consumer.v3

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Stores state: partition of file groupings.

Operator supports running with snapshots only when it reads data using partitions, and when you use it with Structured Data Producer operators.

</td>
</tr>
<tr>
<td valign="top">

Structured Data Operators

</td>
<td valign="top">

Structured File Producer

</td>
<td valign="top">

com.sap.storage.producer.v3

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Operator supports running with snapshots only when you use it with Structured Data Consumer operators with source partitions. However, the operator doesn't support snapshots when you use it with other consumer operators, like ABAP Readers.

</td>
</tr>
<tr>
<td valign="top">

Utilities

</td>
<td valign="top">

Binary to Table

</td>
<td valign="top">

com.sap.table.decode.v2

</td>
<td valign="top">

Yes

</td>
<td valign="top">

None

</td>
</tr>
<tr>
<td valign="top">

Utilities

</td>
<td valign="top">

Table to Binary

</td>
<td valign="top">

comsaap.table.encode

</td>
<td valign="top">

Yes

</td>
<td valign="top">

None

</td>
</tr>
<tr>
<td valign="top">

Utilities

</td>
<td valign="top">

Graph Terminator

</td>
<td valign="top">

com.sap.util.graphTerminator.v2

</td>
<td valign="top">

Yes

</td>
<td valign="top">

None

</td>
</tr>
<tr>
<td valign="top">

Utilities

</td>
<td valign="top">

Terminal

</td>
<td valign="top">

com.sap.util.terminal.v2

</td>
<td valign="top">

With conditions

</td>
<td valign="top">

Data that entered the terminal can be lost when it wasn't processed downstream before a pause or restart.

</td>
</tr>
<tr>
<td valign="top">

Utilities

</td>
<td valign="top">

Wiretap

</td>
<td valign="top">

com.sap.util.wiretap.v2

</td>
<td valign="top">

Yes

</td>
<td valign="top">

None

</td>
</tr>
</table>



<a name="loiof206c726e6d447f5b4df22a2d5ffe7b1__section_hkw_lxf_svb"/>

## Limitations

SAP Data Intelligence doesn't support the following scenarios with the snapshot feature:

-   Circular pipelines: You can't have a pipeline that has a circular connection, which is when the last operator outputs data to the first operator.
-   Debug mode: You can't run graphs in debug mode with snapshots enabled.
-   Group multiplicity: You can't have snapshot generation on graphs with groups that have multiplicity.
-   Subgraphs: You can't create subgraphs for Gen2 pipelines.

**Related Information**  


[State Management](../using-operators/state-management-1d2d1aa.md "Use the state management feature by implementing a series of functions in the Python3 operator.")

[Examples: Operator States](../using-operators/examples-operator-states-a2269e1.md "This section contains examples illustrating the use of state management functions in the Python3 operator for graph snapshots and operator states for Gen2 graphs.")

