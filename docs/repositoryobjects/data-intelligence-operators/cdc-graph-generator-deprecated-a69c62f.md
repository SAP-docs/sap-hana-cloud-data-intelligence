<!-- loioa69c62fbe76547e4b88617b2a0e7f700 -->

# CDC Graph Generator \(Deprecated\)

Change Data Capture is a Delta Capture Technique using database-specific triggers for Insert, Update and Delete. Since manually creating the SQL per table is time consuming, this operator simplifies this.



> ### Note:  
> This operator is deprecated. Use the [Table Replicator V3 \(Deprecated\)](table-replicator-v3-deprecated-79fcadb.md) operator instead.

This operator will require the source Database connection and source table, and the target connection and target specific properties. The operator does static analysis of the metadata of the source table and creates the SQL script for the given database to create shadow table, triggers, view, and few procedures, and so on. Based on these, the operator generates three graphs.

> ### Note:  
> Because this operator does only static analysis, the generated SQL Script needs to be evaluated by your DBA before running the graphs.


<table>
<tr>
<th valign="top">

Port

</th>
<th valign="top">

Description

</th>
<th valign="top">

Path

</th>
</tr>
<tr>
<td valign="top">

outTriggersGraph

</td>
<td valign="top">

Graph with DDL to create triggers on source system

</td>
<td valign="top">

`/vrep/vflow/graphs/com/sap/cdc/initializeTrigger/graph.json` 

</td>
</tr>
<tr>
<td valign="top">

outInitialLoadGraph

</td>
<td valign="top">

Graph to do initial load from source to target

</td>
<td valign="top">

`/vrep/vflow/graphs/com/sap/cdc/initialLoad/graph.json` 

</td>
</tr>
<tr>
<td valign="top">

outDeltaGraph

</td>
<td valign="top">

Graph with delta capture logic

</td>
<td valign="top">

`/vrep/vflow/graphs/com/sap/cdc/delta/graph.json` 

</td>
</tr>
</table>

The graphs will be generated based on the *Path* configuration of Write File operator. Modify that if you want the graph to be generated under different location.



<a name="loioa69c62fbe76547e4b88617b2a0e7f700__section_rc2_5jd_hjb"/>

## Supported Sources

-   DB2

-   HANA

-   MySQL

-   Microsoft SQL Server

-   Oracle


> ### Note:  
> The following source-specific SQL Privileges are required. Ensure the connection user has the following privileges.
> 
> -   CREATE TABLE
> 
> -   CREATE VIEW
> 
> -   CREATE SEQUENCE
> 
> -   CREATE PROCEDURE
> 
> -   CREATE TRIGGER



<a name="loioa69c62fbe76547e4b88617b2a0e7f700__section_ipb_lkd_hjb"/>

## Supported Targets

-   Databases \(HANA\)

-   Cloud Storage \(ADL, WASB, S3, Alibaba Cloud OSS, GCS, HDFS\)

-   Local File system \(local\)




## Modes

For HANA as target we support two modes:

-   Track Change History

-   Apply Change Data




<a name="loioa69c62fbe76547e4b88617b2a0e7f700__section_jzx_rkd_hjb"/>

## Limitations

-   Schema changes \(for example, changes through DDLs\) are not supported.

-   Truncate Table operation is not supported.




<a name="loioa69c62fbe76547e4b88617b2a0e7f700__section_tdk_5kd_hjb"/>

## Delta Graph Logic

Several methods exist to capture the changes in a source table: timestamp based, native CDC, log reading, and so on. Native CDC methods with transactional consistency are difficult to scale due to their atomicity nature. For SAP Data Intelligence purposes, where the data volume can be significantly higher for certain tables, we propose to use triggers. Note that `trigger` is the only method that is supported for all databases.

To achive this, we created the following objects in the source schema.


<table>
<tr>
<th valign="top">

Object

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

srcTable\_CLEANUP

</td>
<td valign="top">

PROCEDURE

</td>
<td valign="top">

Initial procedure that will drop existing triggers and other database objects created for this srcTable.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SEQUENCE

</td>
<td valign="top">

SEQUENCE

</td>
<td valign="top">

Some databases will use a SEQUENCE to generate an increasing ID.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SHADOW

</td>
<td valign="top">

TABLE

</td>
<td valign="top">

Shadow table that will be used for storing the delta records along with transaction type.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_TRIGGER\_QUEUE

</td>
<td valign="top">

TABLE

</td>
<td valign="top">

Queue table that will be used for marking the records from shadow table for replication.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SHADOW\_VIEW

</td>
<td valign="top">

VIEW

</td>
<td valign="top">

View that inner joins the marked records from queue table with shadow table.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_CHECKPOINT

</td>
<td valign="top">

TABLE

</td>
<td valign="top">

Checkpoint table is used to indicate when we began replication and when we completed the delta.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_INSERT\_TRIGGER

</td>
<td valign="top">

TRIGGER

</td>
<td valign="top">

Insert trigger.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_DELETE\_TRIGGER

</td>
<td valign="top">

TRIGGER

</td>
<td valign="top">

Delete trigger.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_UPDATE\_TRIGGER

</td>
<td valign="top">

TRIGGER

</td>
<td valign="top">

Insert trigger.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_INITIAL\_SHADOW\_SCAN

</td>
<td valign="top">

PROCEDURE

</td>
<td valign="top">

Procedure to determine when the graph should stop running.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SHADOW\_SCAN

</td>
<td valign="top">

PROCEDURE

</td>
<td valign="top">

Procedure to mark shadow table records into queue table.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SHADOW\_CHECKPOINT

</td>
<td valign="top">

PROCEDURE

</td>
<td valign="top">

Procedure to update timestamp on checkpoint table.

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SHADOW\_CLNEAUP

</td>
<td valign="top">

PROCEDURE

</td>
<td valign="top">

Procedure to cleanup shadow and queue table both.

</td>
</tr>
</table>

When you create the trigger on the source, any changes happening to the source table are replicated in the shadow table.

When you trigger the delta graph, the following actions happen:

-   srcTable\_SHADOW\_SCAN procedure is called on the source, which will copy the current records from the shadow table to the queue table.

-   The records in the queue table have a load status \(indicating whether the records were loaded to target or not\).

-   Table Consumer will read the data from the view only the records that are in queue table and will load to target.

-   srcTable\_SHADOW\_CHECKPOINT procedure is called to update the load status of the records in the queue table.

-   srcTable\_SHADOW\_CLEANUP is called to delete the records that were successfully loaded to target from queue and shadow tables.




<a name="loioa69c62fbe76547e4b88617b2a0e7f700__section_vjz_jmd_hjb"/>

## Configuration parameters

The following parameters can or must \(\*\) be provided to execute a data transfer.


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

source\*

</td>
<td valign="top">

Source system

</td>
</tr>
<tr>
<td valign="top">

target\*

</td>
<td valign="top">

Target system

</td>
</tr>
<tr>
<td valign="top">

Delta Graph Run Mode\*

</td>
<td valign="top">

Polling Interval vs Manual

</td>
</tr>
<tr>
<td valign="top">

Delta Batch Size\*

</td>
<td valign="top">

How many rows will be fetched per polling period

</td>
</tr>
<tr>
<td valign="top">

Tablespace

</td>
<td valign="top">

Tablespace where the `SHADOW` and `TRIGGER_QUEUE` tables should be created

</td>
</tr>
</table>

Based on the source or target system the configuration is based on. See the Table Consumer operators for your source, [Flowagent File Producer \(Deprecated\)](flowagent-file-producer-deprecated-76e9d5c.md), and [Flowagent Table Producer \(Deprecated\)](flowagent-table-producer-deprecated-fda7323.md).



<a name="loioa69c62fbe76547e4b88617b2a0e7f700__section_nck_gnd_hjb"/>

## Delta Graph Run Mode

-   Polling Interval: In this mode, delta graph runs every N seconds. Use this mode if the source table changes frequently. In this mode, the delta graph pod runs forever. It will first run the first delta job, then wait N seconds and trigger the delta job again.

-   Manual: The graph terminates after running once. Use this mode if the source is does not change frequently. Running once only can save pod resources when not running. This is also useful when you have multiple tables to replicate. For example, say that you have 100 tables in the sources. Ten of those are changing frequently, while the remaining 90 are updated less frequently. To utilize the pod resources efficiently, one can have the frequent tables' graph running indefinitely, and the remaining 90 tables delta graphs can be chained in another workflow graph. That way, only one pod, is used and it will run the delta graph first, and then the second, and so on.




<a name="loioa69c62fbe76547e4b88617b2a0e7f700__section_fyn_4nd_hjb"/>

## Input


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

input

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The input signal received from an another operator that can be used as a trigger. You can always use Constant Generator to trigger this operator.

</td>
</tr>
</table>



<a name="loioa69c62fbe76547e4b88617b2a0e7f700__section_htz_snd_hjb"/>

## Output


<table>
<tr>
<th valign="top">

Output

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

outTriggersGraph

</td>
<td valign="top">

string

</td>
<td valign="top">

The graph for triggers creation.

</td>
</tr>
<tr>
<td valign="top">

outInitialLoadGraph

</td>
<td valign="top">

string

</td>
<td valign="top">

The graph for doing the initial load of data from the source to target.

</td>
</tr>
<tr>
<td valign="top">

outDeltaGraph

</td>
<td valign="top">

string

</td>
<td valign="top">

The graph for delta capture logic to capture changes from the source to target.

</td>
</tr>
</table>



<a name="loioa69c62fbe76547e4b88617b2a0e7f700__section_cz2_b4d_hjb"/>

## Additional Information

-   Connect this operator to the Trigger/Constant Generator or Terminator operator if it is the first or last operator that you want to be executed.

-   During the execution, it will create multiple graphs but not execute them.

-   Validate and optimize the generated graphs before running things to consider are.

-   Changing the fetchSize for the consumer \(wide tables use a lower number like 100, narrow tables use a higher number\).

-   Adding a logical partition in the consumer, and grouping the producer to run the initial load in parallel.

-   Because this operator will do only static analysis, the generated SQL Script needs to be evaluated by your DBA before running the graph on a production database.


**Related Information**  


[Improving CDC Graph Generator Operator Performance](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/8709ef1f2c03489eb404496f20484411.html "The performance of the Change Data Capture (CDC) Graph Generator operator depends on the initial table size and how rapidly change data is generated in the source system.") :arrow_upper_right:

[Changing Data Capture (CDC)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/023c75aedfdd4646934f2d9ccde5660a.html "SAP Data Intelligence supports CDC technology for some connection types.") :arrow_upper_right:

 <?sap-ot O2O class="- topic/link " href="93b5e5391e304c59996e4ba45cb7c422.xml" text="" desc="" xtrc="topicref:8" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/440b12d97aad47b89619fface51f871e.ditamap" ?> 

