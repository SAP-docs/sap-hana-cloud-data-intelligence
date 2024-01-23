<!-- loio79fcadb91f584f868a6662111b92f6e7 -->

# Table Replicator V3 \(Deprecated\)

Change Data Capture \(CDC\) is a delta capture technique that uses triggers for Insert, Update, and Delete to track the change history for a specific table. This operator is supported in Generation 1 graphs.



In addition to capturing the delta, this operator also handles applying the changes to a target table, allowing replication of tables in an efficient and secure way through an in-built recovery mechanism.

Depending on the selected execution mode, this operator performs one of the following operations:

-   Delta: At first, it creates all necessary triggers in the source, and then performs an initial load. For consecutive executions, it only extracts delta records created since the last run.
-   Clean-up: It removes all previously created triggers, procedures, and tables in the source.

> ### Caution:  
> Support for Microsoft Azure Data Lake Storage Gen1 \(ADL\) in this operator is deprecated.



<a name="loio79fcadb91f584f868a6662111b92f6e7__section_brm_wlw_dlb"/>

## Supported Sources

-   Microsoft Azure SQL Database
-   IBM DB2
-   SAP HANA
-   MySQL
-   Microsoft SQL Server
-   Oracle

> ### Note:  
> The following source-specific SQL Privileges are required. Ensure that the connection user has the following privileges:
> 
> -   CREATE TABLE
> -   CREATE VIEW
> -   CREATE SEQUENCE
> -   CREATE PROCEDURE
> -   CREATE TRIGGER
> 
> If you use a custom schema to create the tables, views, sequences, and procedures, then the connection user must have the above privileges in the custom schema. The connection user does not need the CREATE TRIGGER or SELECT privileges, which must be in the schema of the original table. For details about database privileges, see the **Using a Custom Schema on Table Replicator** section at the end of this topic.



<a name="loio79fcadb91f584f868a6662111b92f6e7__section_gm1_2mw_dlb"/>

## Supported Targets

-   Databases: SAP HANA \(HANA\)
-   Cloud Storage: Microsoft Azure Storage Blob \(WASB\), Amazon Simple Storage Service \(S3\), Alibaba Cloud Object Storage Service \(OSS\), Google Cloud Storage \(GCS\), Hadoop Distributed File System \(HDFS\)
-   Local file system \(local\)



<a name="loio79fcadb91f584f868a6662111b92f6e7__section_w34_gmw_dlb"/>

## Modes

For HANA as a target, two modes are supported:

-   Track Change History
-   Apply Change Data

When using Apply Change Data, you can either copy primary keys only or all columns. When you select primary keys only, the created triggers are faster and create less impact on the source, but the replication is slower. When all columns are selected, the created triggers are slower but the replication is faster.

For other targets, only **Track Change History** is supported.



## Limitations

-   Schema Changes \(for example, changes through DDLs\) are not supported
-   LZO compression is not supported for Parquet files



<a name="loio79fcadb91f584f868a6662111b92f6e7__section_wjj_lmw_dlb"/>

## Migration

If triggers and procedures have already been created for a given table by the CDC Graph Generator \(`com.sap.cdc.graphGenerator`\) operator, then it's necessary to either stick to the generated delta graph to do the delta processing, or execute this operator in **Clean Up** execution mode to remove all triggers and procedures for a given source table. You would run it again in **Delta** execution mode.

> ### Caution:  
> This action drops all nonapplied shadow records.



<a name="loio79fcadb91f584f868a6662111b92f6e7__section_cc2_rmw_dlb"/>

## Operator Usage

CDC performance depends on the initial table size and how rapidly change data is generated in the source table. To optimize and process different scenarios, here are some helpful points on using this operator.

-   Initial Load Volume
    -   If the source table is large, you can partition the source data using the **Partition Specification** property. After the partitions are defined based on the resources available, you can set the **Max Number of Loaders** property to an appropriate value \(default is `8`\).


-   Delta Change Rate
    -   For rapidly changing tables, we recommended setting the **Delta Graph Run Mode** field under the **Delta Load Properties** property to **Polling Interval**, with a short **Max Polling Interval**. This way, the operator runs continuously, fetching the data in short intervals.
    -   For slowly changing tables, one can either set the **Delta Graph Run Mode** field to `Manual` and schedule the graph to run periodically \(every N hours\), or set the *Delta Graph Run Mode* to `Polling Interval` with high `Max Polling Interval`. When `Polling Interval` is used, the graph runs continuously, while in Manual mode the graph fetches the delta records once and then stops processing. You can then terminate the graph connecting the output of this operator to a graph terminator.




<a name="loio79fcadb91f584f868a6662111b92f6e7__section_cbk_wmw_dlb"/>

## Tracking Multiple Tables

This operator handles a single table at a time. If it is necessary to track multiple tables, create an instance of this operator for each source-target pair. However, if each operator runs in a separate graph, it uses a lot of storage, because each graph has at least one additional pod. Here are some strategies to reduce resource usage. Consider the example below:

> ### Example:  
> You have 10 source tables. Two of them are rapidly changing while the other eight are slowly changing.

For rapidly changing tables \(see the Operator Usage section above\), you should create one graph per table. This graph should be run forever in **Polling Interval** mode with short **Max Polling Interval**.

For the slowly changing tables, you can chain this operator multiple times, one after another in the same graph. While chaining this operator, set the *Delta Graph Run Mode* to `Manual`. This setting means that when the first operator completes its data movement, the second one is started, and so on. While chaining, you can group every N operators \(recommended: 5\), so that each group runs in their own pod. To save further resource usage, schedule this graph based on the delta change rate on the source \(see the Operator Usage section above\). This way, you are not consuming resources for slowly changing tables or reducing the number of used SQL connections to the source.

> ### Note:  
> -   The recommended group resource is 0.5 CPU and 1500 m memory. More than two CPUs are not helpful for processing. However, more RAM \(max is 4 GB\) is better when the operators are chained.
> 
> -   RAM requirements are based on the defined *Source Fetch Size* and *Target Batch Size*.
>     -   For wide tables \(over 100 columns\), a smaller fetch size is better \(<1000\) and higher RAM value.
>     -   For narrow tables, a larger fetch size gives better throughput.
> 
> -   During delta processing, a maximum of two SQL connections are required for each source table. However, during the initial load, we use 1 + *Max Number of Loaders* connections.



<a name="loio79fcadb91f584f868a6662111b92f6e7__section_i4h_hnw_dlb"/>

## Delta Extraction Logic

Several methods exist to capture the changes of a source table. Timestamp-based, native CDC, log-based reading, and so on. Native CDC methods with transactional consistency are difficult to scale due to their atomicity nature. For Data Intelligence purposes where the data volume can be significantly higher for certain tables, we recommend using triggers. Note that trigger is the only method that is supported for all databases.

To capture the changes of a source table, a few objects are created in the source schema.


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

srcTable\_ICL

</td>
<td valign="top">

PROCEDURE

</td>
<td valign="top">

Procedure to drop all auxiliary objects created for the delta extraction logic

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SEQ

</td>
<td valign="top">

SEQUENCE

</td>
<td valign="top">

A sequence used to generate an operation ID for each delta record

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SHA

</td>
<td valign="top">

TABLE

</td>
<td valign="top">

Shadow table used to store the delta records

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SHV

</td>
<td valign="top">

VIEW

</td>
<td valign="top">

View that displays the current batch of delta records in the shadow table

</td>
</tr>
<tr>
<td valign="top">

srcTable\_CHK

</td>
<td valign="top">

TABLE

</td>
<td valign="top">

Checkpoint table used to flag some values necessary for the replication process, such as flagging the timestamp of when the replication began, or the number delta records that have been applied so far

</td>
</tr>
<tr>
<td valign="top">

srcTable\_INS

</td>
<td valign="top">

TRIGGER

</td>
<td valign="top">

Insert Trigger

</td>
</tr>
<tr>
<td valign="top">

srcTable\_DEL

</td>
<td valign="top">

TRIGGER

</td>
<td valign="top">

Delete Trigger

</td>
</tr>
<tr>
<td valign="top">

srcTable\_UPD

</td>
<td valign="top">

TRIGGER

</td>
<td valign="top">

Update Trigger

</td>
</tr>
<tr>
<td valign="top">

srcTable\_ISS

</td>
<td valign="top">

PROCEDURE

</td>
<td valign="top">

Procedure to set some flags in the srcTable\_CHECKPOINT table

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SCB

</td>
<td valign="top">

PROCEDURE

</td>
<td valign="top">

Procedure to mark shadow table records to be extracted

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SCE

</td>
<td valign="top">

PROCEDURE

</td>
<td valign="top">

Procedure to mark shadow table records to be deleted

</td>
</tr>
<tr>
<td valign="top">

srcTable\_SCL

</td>
<td valign="top">

PROCEDURE

</td>
<td valign="top">

Procedure to remove records from shadow table

</td>
</tr>
</table>

Given those objects, the delta extraction logic happens as follows:

1.  The triggers capture all changes in the source table and copy them to the `srcTable_SHADOW` table.
2.  A graph containing this operator is started.
3.  This operator calls the `srcTable_INITIAL_SHADOW_SCAN` procedure to set some flags in the `srcTable_CHECKPOINT` table.
4.  This operator calls the `srcTable_SHADOW_CHECKPOINT_BEGIN` procedure to mark a batch of records in the shadow table to be extracted.
5.  An ingestion job is started to apply all records in the `srcTable_SHADOW_VIEW` to the target.
6.  This operator calls the `srcTable_SHADOW_CHECKPOINT_END` procedure to mark all records in `srcTable_SHADOW` table previously marked to be extracted now to be deleted.
7.  This operator calls the `srcTable_SHADOW_CLEANUP` to remove all records in the `srcTable_SHADOW` table that are marked for deletion.



## Configuration Parameters


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

ID

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

Execution Mode

</td>
<td valign="top">

executionMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Choose an operation.

-   Delta: Apply all delta records from source to target since the last execution.
-   Clean Up: Remove all temporary objects and triggers created in the source.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Source

</td>
<td valign="top">

source

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Database of the source table. Supported databases are displayed below.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Source Azure SQL DB Connection

</td>
<td valign="top">

azuresqldbConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to an Azure SQL DB database.

</td>
</tr>
<tr>
<td valign="top">

Source DB2 Connection

</td>
<td valign="top">

db2Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a DB2 database.

</td>
</tr>
<tr>
<td valign="top">

Source HANA Connection

</td>
<td valign="top">

hanaConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a HANA database.

</td>
</tr>
<tr>
<td valign="top">

Source MSSQL Connection

</td>
<td valign="top">

mssqlConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to an MSSQL database.

</td>
</tr>
<tr>
<td valign="top">

Source MySQL Connection

</td>
<td valign="top">

mysqlConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a MySQL database.

</td>
</tr>
<tr>
<td valign="top">

Source Oracle Connection

</td>
<td valign="top">

oracleConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to an Oracle database.

</td>
</tr>
<tr>
<td valign="top">

Source Azure SQL DB Table

</td>
<td valign="top">

azuresqldbAdaptedDataset

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. Source Azure SQL DB table from which the delta data is read.

</td>
</tr>
<tr>
<td valign="top">

Source DB2 Table

</td>
<td valign="top">

db2AdaptedDataset

</td>
<td valign="top">

object

</td>
<td valign="top">

Source DB2 table from which the delta data is read.

</td>
</tr>
<tr>
<td valign="top">

Source HANA Table

</td>
<td valign="top">

hanaAdaptedDataset

</td>
<td valign="top">

object

</td>
<td valign="top">

Source HANA table from which the delta data is read.

</td>
</tr>
<tr>
<td valign="top">

Source MSSQL Table

</td>
<td valign="top">

mssqlAdaptedDataset

</td>
<td valign="top">

object

</td>
<td valign="top">

Source MSSQL table from which the delta data is read.

</td>
</tr>
<tr>
<td valign="top">

Source MySQL Table

</td>
<td valign="top">

mysqlAdaptedDataset

</td>
<td valign="top">

object

</td>
<td valign="top">

Source MySQL table from which the delta data is read.

</td>
</tr>
<tr>
<td valign="top">

Source Oracle Table

</td>
<td valign="top">

oracleAdaptedDataset

</td>
<td valign="top">

object

</td>
<td valign="top">

Source Oracle table from which the delta data is read.

</td>
</tr>
<tr>
<td valign="top">

Azure SQL DB Partition Type

</td>
<td valign="top">

azuresqldbPartitionType

</td>
<td valign="top">

string

</td>
<td valign="top">

To load the data in parallel, partition the source data during the initial load.

Default: "None":

</td>
</tr>
<tr>
<td valign="top">

Azure SQL DB Logical Partition Specification

</td>
<td valign="top">

azuresqldbPartitionSpecification

</td>
<td valign="top">

object

</td>
<td valign="top">

For more information, see [Partitioning](partitioning-86085d9.md).

</td>
</tr>
<tr>
<td valign="top">

Azure SQL DB Max Number of Loaders

</td>
<td valign="top">

azuresqldbMultiplicity

</td>
<td valign="top">

integer

</td>
<td valign="top">

Defines the maximum number of parallel loaders during the initial load. Each parallel loader is equivalent to a pod. The final number of loaders is equal to the minimum \(maximum number of loaders, number of partitions\).

Default: 8

</td>
</tr>
<tr>
<td valign="top">

DB2 Partition Type

</td>
<td valign="top">

db2PartitionType

</td>
<td valign="top">

string

</td>
<td valign="top">

To load the data in parallel, partition the source data during the initial load.

Default: "None"

</td>
</tr>
<tr>
<td valign="top">

DB2 Logical Partition Specification

</td>
<td valign="top">

db2PartitionSpecification

</td>
<td valign="top">

object

</td>
<td valign="top">

For more information, see [Partitioning](partitioning-86085d9.md).

</td>
</tr>
<tr>
<td valign="top">

DB2 Max Number of Loaders

</td>
<td valign="top">

db2Multiplicity

</td>
<td valign="top">

integer

</td>
<td valign="top">

Defines the maximum number of parallel loaders during the initial load. Each parallel loader is equivalent to a pod. The final number of loaders is equal to the minimum \(maximum number of loaders, number of partitions\).

Default: 8

</td>
</tr>
<tr>
<td valign="top">

HANA Partition Type

</td>
<td valign="top">

hanaPartitionType

</td>
<td valign="top">

string

</td>
<td valign="top">

To load the data in parallel, partition the source data during the initial load.

</td>
</tr>
<tr>
<td valign="top">

HANA Logical Partition Specification

</td>
<td valign="top">

hanaPartitionSpecification

</td>
<td valign="top">

object

</td>
<td valign="top">

For more information, see [Partitioning](partitioning-86085d9.md).

</td>
</tr>
<tr>
<td valign="top">

HANA Max Number of Loaders

</td>
<td valign="top">

hanaMultiplicity

</td>
<td valign="top">

integer

</td>
<td valign="top">

Defines the maximum number of parallel loaders during the initial load. Each parallel loader is equivalent to a pod. The final number of loaders is equal to the minimum \(maximum number of loaders, number of partitions\).

Default: 8

</td>
</tr>
<tr>
<td valign="top">

MySQL Partition Type

</td>
<td valign="top">

mysqlPartitionType

</td>
<td valign="top">

string

</td>
<td valign="top">

To load the data in parallel, partition the source data during the initial load.

Default: "None"

</td>
</tr>
<tr>
<td valign="top">

MySQL Logical Partition Specification

</td>
<td valign="top">

mysqlPartitionSpecification

</td>
<td valign="top">

object

</td>
<td valign="top">

For more information, see [Partitioning](partitioning-86085d9.md).

</td>
</tr>
<tr>
<td valign="top">

MySQL Max Number of Loaders

</td>
<td valign="top">

mysqlMultiplicity

</td>
<td valign="top">

integer

</td>
<td valign="top">

Defines the maximum number of parallel loaders during the initial load. Each parallel loader is equivalent to a pod. The final number of loaders is equal to the minimum \(maximum number of loaders, number of partitions\).

Default: 8

</td>
</tr>
<tr>
<td valign="top">

MSSQL Partition Type

</td>
<td valign="top">

mssqlPartitionType

</td>
<td valign="top">

string

</td>
<td valign="top">

To load the data in parallel, partition the source data during the initial load.

</td>
</tr>
<tr>
<td valign="top">

MSSQL Logical Partition Specification

</td>
<td valign="top">

mssqlPartitionSpecification

</td>
<td valign="top">

object

</td>
<td valign="top">

For more information, see [Partitioning](partitioning-86085d9.md).

</td>
</tr>
<tr>
<td valign="top">

MSSQL Max Number of Loaders

</td>
<td valign="top">

mssqlMultiplicity

</td>
<td valign="top">

integer

</td>
<td valign="top">

Defines the maximum number of parallel loaders during the initial load. Each parallel loader is equivalent to a pod. The final number of loaders is equal to the minimum \(maximum number of loaders, number of partitions\).

Default: 8

</td>
</tr>
<tr>
<td valign="top">

Oracle Partition Type

</td>
<td valign="top">

oraclePartitionType

</td>
<td valign="top">

string

</td>
<td valign="top">

To load the data in parallel, partition the source data during the initial load.

Default: "None"

</td>
</tr>
<tr>
<td valign="top">

Oracle Logical Partition Specification

</td>
<td valign="top">

oraclePartitionSpecification

</td>
<td valign="top">

object

</td>
<td valign="top">

For more information, see [Partitioning](partitioning-86085d9.md).

</td>
</tr>
<tr>
<td valign="top">

Oracle Number of partitions

</td>
<td valign="top">

oracleNumberOfPartitions

</td>
<td valign="top">

integer

</td>
<td valign="top">

When partition type is set to *Row ID*, specify the number of ranges in the table for partitioning.

</td>
</tr>
<tr>
<td valign="top">

Oracle Max Number of Loaders

</td>
<td valign="top">

oracleMultiplicity

</td>
<td valign="top">

integer

</td>
<td valign="top">

Defines the maximum number of parallel loaders during the initial load. Each parallel loader is equivalent to a pod. The final number of loaders is equal to the minimum \(maximum number of loaders, number of partitions\).

</td>
</tr>
<tr>
<td valign="top">

Source Tablespace

</td>
<td valign="top">

tablespace

</td>
<td valign="top">

string

</td>
<td valign="top">

Tablespace where auxiliary tables are created

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Source Fetch Size

</td>
<td valign="top">

fetchSize

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the number of rows fetched from the source in each request. For wide tables, smaller values are better. For tables with fewer columns , larger values are better.

Default: 1000

</td>
</tr>
<tr>
<td valign="top">

Custom Schema

</td>
<td valign="top">

tempSchema

</td>
<td valign="top">

string

</td>
<td valign="top">

Schema where the auxiliary tables, sequences, and procedures are created. The user who runs the Table Replicator doesn’t need to have privileges on the original schema. The CREATE TABLE, CREATE VIEW, CREATE SEQUENCE, and CREATE PROCEDURE privileges are only needed on the custom schema, not in the schema of the original table. However, the CREATE TRIGGER and SELECT privileges are still needed on the original schema. For information about database privileges, see the **Using a Custom Schema on Table Replicator** section at the end of this documentation.

</td>
</tr>
<tr>
<td valign="top">

Target

</td>
<td valign="top">

target

</td>
<td valign="top">

string

</td>
<td valign="top">

System of the target table or file. Supported systems are displayed below.

</td>
</tr>
<tr>
<td valign="top">

Target HANA Connection

</td>
<td valign="top">

hanaTargetConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a HANA database.

</td>
</tr>
<tr>
<td valign="top">

Target HANA Wire port

</td>
<td valign="top">

hanaWiredPort

</td>
<td valign="top">

string

</td>
<td valign="top">

HANA Wire port of the transaction coordinator, which is determined as `3XX15`, where XX is the instance number of the cluster as configured in the Kubernetes cluster manager.

Default: "30115"

</td>
</tr>
<tr>
<td valign="top">

Target ADL Connection

</td>
<td valign="top">

adlTargetConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to an ADL storage.

</td>
</tr>
<tr>
<td valign="top">

Target SDL Connection

</td>
<td valign="top">

sdlTargetConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to an SDL storage.

</td>
</tr>
<tr>
<td valign="top">

Target HDFS Connection

</td>
<td valign="top">

hdfsTargetConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a HDFS storage.

</td>
</tr>
<tr>
<td valign="top">

Target GCS Connection

</td>
<td valign="top">

gcsTargetConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a GCS storage.

</td>
</tr>
<tr>
<td valign="top">

Target S3 Connection

</td>
<td valign="top">

s3TargetConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a S3 storage.

</td>
</tr>
<tr>
<td valign="top">

Target OSS Connection

</td>
<td valign="top">

ossTargetConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to an OSS storage.

</td>
</tr>
<tr>
<td valign="top">

Target WASB Connection

</td>
<td valign="top">

wasbTargetConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a WASB storage.

</td>
</tr>
<tr>
<td valign="top">

Target HANA Table

</td>
<td valign="top">

hanaTargetAdaptedDataset

</td>
<td valign="top">

object

</td>
<td valign="top">

Target HANA table where the delta data is written.

</td>
</tr>
<tr>
<td valign="top">

Target ADL File

</td>
<td valign="top">

adlTargetObjectName

</td>
<td valign="top">

string

</td>
<td valign="top">

Target ADL file where the delta data is written. It is required to use <timestamp\> as part of the file name to ensure that each delta batch has a unique file name.

</td>
</tr>
<tr>
<td valign="top">

Target SDL File

</td>
<td valign="top">

sdlTargetObjectName

</td>
<td valign="top">

string

</td>
<td valign="top">

Target ADL file where the delta data is written. It is required to use <timestamp\> as part of the file name to ensure that each delta batch has a unique file name.

</td>
</tr>
<tr>
<td valign="top">

Target HDFS File

</td>
<td valign="top">

hdfsTargetObjectName

</td>
<td valign="top">

string

</td>
<td valign="top">

Target HDFS file where the delta data is written. It is required to use <timestamp\> as part of the file name to ensure that each delta batch has a unique file name.

</td>
</tr>
<tr>
<td valign="top">

Target GCS File

</td>
<td valign="top">

gcsTargetObjectName

</td>
<td valign="top">

string

</td>
<td valign="top">

Target GCS file where the delta data is written. It is required to use <timestamp\> as part of the file name to ensure that each delta batch has a unique file name.

</td>
</tr>
<tr>
<td valign="top">

Target S3 File

</td>
<td valign="top">

s3TargetObjectName

</td>
<td valign="top">

string

</td>
<td valign="top">

Target S3 where the delta data is written. It is required to use <timestamp\> as part of the file name to ensure that each delta batch has a unique file name.

</td>
</tr>
<tr>
<td valign="top">

Target OSS File

</td>
<td valign="top">

ossTargetObjectName

</td>
<td valign="top">

string

</td>
<td valign="top">

Target OSS file where the delta data is written. It is required to use <timestamp\> as part of the file name to ensure that each delta batch has a unique file name.

</td>
</tr>
<tr>
<td valign="top">

Target WASB File

</td>
<td valign="top">

wasbTargetObjectName

</td>
<td valign="top">

string

</td>
<td valign="top">

Target WASB file where the delta data is written. It is required to use <timestamp\> as part of the file name to ensure that each delta batch has a unique file name.

</td>
</tr>
<tr>
<td valign="top">

Target Local File

</td>
<td valign="top">

path

</td>
<td valign="top">

string

</td>
<td valign="top">

A formatted string describing the output path and file name. If the root directory of the file is not provided, “/vrep/” is used as default root directory of the file. It is required to use <timestamp\> as part of the file name to ensure that each delta batch has a unique file name.

Default: /vrep/<sourceTableName\>\_<timestamp\>.csv

</td>
</tr>
<tr>
<td valign="top">

Target Write Mode

</td>
<td valign="top">

mode

</td>
<td valign="top">

string

</td>
<td valign="top">

The write mode for the target table during initial load. If set to *overwrite*, the table is dropped and recreated. When set to *truncate*, all data is deleted from table. When set to *append* the data from the source is appended..

Default: "overwrite"

</td>
</tr>
<tr>
<td valign="top">

Target Format

</td>
<td valign="top">

format

</td>
<td valign="top">

string

</td>
<td valign="top">

Output file format: CSV, PARQUET, and ORC are supported for the cloud storages. The CSV that is produced conforms to the RFC-4180 specification, where the row delimiter is always CRLF and the escape character is always double quotes. Currently, only CSV is supported for local storage.

Default: "CSV"

</td>
</tr>
<tr>
<td valign="top">

Target CSV Properties

</td>
<td valign="top">

additionalProperties\_csv

</td>
<td valign="top">

object

</td>
<td valign="top">

Properties of the CSV output:

-   Column delimiter \(ID columnDelimiter; type string\): The field separator. Only the following characters are supported: “,”, “;”, “|”, “:” and “TAB”.

    Default: ","

-   Header Included \(ID csvHeaderIncluded; type boolean\): Indicates whether each CSV output has a header as first line.

    Default: false




</td>
</tr>
<tr>
<td valign="top">

Additional Properties

</td>
<td valign="top">

additionalProperties\_common

</td>
<td valign="top">

object

</td>
<td valign="top">

Additional properties related to the upload options to cloud storage. It is only applicable when a cloud storage service is selected.

-   Compression Type \(ID compressionType; type string\): Compression type used when uploading file into cloud service. LZO compression is not supported for PARQUET files.

    Default "None"




</td>
</tr>
<tr>
<td valign="top">

Delta Load Properties

</td>
<td valign="top">

deltaProperties

</td>
<td valign="top">

object

</td>
<td valign="top">

Additional properties for delta processing:

-   Change Data Applier Mode \(ID cdcApplierType; type string\): See the delta Processing section in the Flowagent Table Producer operator documentation.

    Default: "Track Change History"

-   Delta Graph Run \(ID deltaGraphMode; type string\): How delta processing is run. In *manual* mode, it counts the number of delta rows in the source at the beginning of the job, and it stops after all rows have been fetched. In *polling interval*, it runs indefinitely.

    Default: "Polling Interval"

-   Capture Only Primary Keys \(ID captureOnlyPrimaryKeys; type boolean\): This option only affects the initial load. When enabled, the created triggers copy the primary keys only to this shadow table, which saves space but results in a slower replication.

    Default: false

-   Capture Only Primary Keys on Delete \(ID captureOnlyPrimaryKeysOnDelete; type boolean\): During a delete operation, the created triggers copy the primary keys only to the shadow table to save space and perform a quicker replication.
-   Capture Only New Values on Update \(ID: captureOnlyNewValueOnUpdate; type boolean\): During an update operation, the created triggers copy the updated value of the modified entry to save space and perform a quicker replication.
-   Max Polling Interval \(ID maxPollingInterval; type number\): When Delta Graph Run Mode is set to *polling interval*, this option defines the max interval on which the polling is performed in seconds.

    Default: 3600

-   Delta Batch Size \(ID deltaBatchSize; type number\): The number of delta rows fetched at a time.

    Default: 100000




</td>
</tr>
<tr>
<td valign="top">

Source table name alias

</td>
<td valign="top">

sourceTableNameAlias

</td>
<td valign="top">

string

</td>
<td valign="top">

The source table name alias, which can be used when there are long identifier issues in the database. When specified, it should be shorter than 28 characters. When not specified, the source table name is used instead. In this process, a helper table called DI\_CDC\_ALIASES is created in the database to store specified suffixes.

</td>
</tr>
</table>



<a name="loio79fcadb91f584f868a6662111b92f6e7__section_r4f_lrx_dlb"/>

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

inTrigger

</td>
<td valign="top">

message

</td>
<td valign="top">

Port to trigger the operator.

</td>
</tr>
</table>



<a name="loio79fcadb91f584f868a6662111b92f6e7__section_g1c_hsx_dlb"/>

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

result

</td>
<td valign="top">

message

</td>
<td valign="top">

The fully qualified name of the target object. It is sent to each consumed delta batch.

-   Body \(Type string\): The fully qualified name of the target object.
-   Attributes:
    -   message.lastBatch \(Type boolean\): Boolean option that indicates the current batch is the last one.
    -   message.batchIndex \(Type int\): Indicates which batch is being processed, starting from 0.
    -   message.executionMode \(Type string\): Execution mode that was performed.

-   Encoding \(Type string\)



</td>
</tr>
<tr>
<td valign="top">

error

</td>
<td valign="top">

message.error

</td>
<td valign="top">

Operator error. If mapped, the operator error is sent to this port and the graph remains running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>



<a name="loio79fcadb91f584f868a6662111b92f6e7__section_kxf_d4x_bpb"/>

## Using a Custom Schema on Table Replicator

The Table Replicator operator creates tables, views, sequences, triggers, and procedures in the database. For security or other reasons, you may want a database user without create privileges on the source schema to be able to run the Table Replicator. To allow a user to run the Table Replicator operator with minimum privileges, you can specify a custom schema on the Table Replicator operator. The objects are created on the custom schema and do not mix with those in the schema of the original table. CREATE TRIGGER and SELECT privileges are still needed on the same schema of the original table.

Due to differences in databases, certain privileges must be defined correctly for the Table Replicator operator to run. To illustrate the differences, let’s say that you want to replicate the table SOURCE of a schema named SOURCE\_SCHEMA, using the custom schema, CUSTOM\_SCHEMA. There are two user types with different privileges, CustomUser and OriginalUser. The CustomUser has a minimum set of privileges needed to use Table Replicator in the CUSTOM\_SCHEMA while OriginalUser has the privileges to run Table Replicator without a custom schema. Also, OriginalUser is able to insert, update and delete records on the table SOURCE.

These are user privileges necessary to run the Table Replicator operator on each database:


<table>
<tr>
<th valign="top">

Database

</th>
<th valign="top">

Privileges

</th>
</tr>
<tr>
<td valign="top">

HANA

</td>
<td valign="top">

CustomUser needs the following privilege on schema CUSTOM\_SCHEMA: CREATE ANY \(so it can create TABLE, VIEW, SEQUENCE, PROCEDURE\). Also user CustomUser needs the following privileges on schema SOURCE\_SCHEMA: TRIGGER, SELECT SQL statements \(assuming the schemas CUSTOM\_SCHEMA, SOURCE\_SCHEMA, the table SOURCE and the user CustomUser already exist\):

GRANT CREATE ANY ON SCHEMA CUSTOM\_SCHEMA TO CustomUser;

GRANT SELECT ON SCHEMA SOURCE\_SCHEMA TO CustomUser;

GRANT TRIGGER ON SCHEMA SOURCE\_SCHEMA TO CustomUser.

</td>
</tr>
<tr>
<td valign="top">

DB2

</td>
<td valign="top">

To create a TRIGGER, you must have the ALTER privilege on the table or the ALTERIN privilege on the schema that the table belongs to. The SELECT privilege must be granted directly to a table. However, according to DB2 documentation, newer versions of DB2 can grant the SELECTIN privilege on a schema. The following SQL statements can make the Table Replicator work properly on the example scenario.

GRANT CREATEIN ON SCHEMA CUSTOM\_SCHEMA TO CustomUser;

GRANT SELECT ON SOURCE\_SCHEMA.SOURCE TO CustomUser;

GRANT ALTERIN ON SCHEMA SOURCE\_SCHEMA TO CustomUser.

</td>
</tr>
<tr>
<td valign="top">

MySQL

</td>
<td valign="top">

The schema is a synonym of the database, so there are no schemas in MySQL; only databases. These privileges are needed to ‘CustomUser’:

GRANT ALL PRIVILEGES ON CUSTOM\_SCHEMA.\* TO CustomUser;

GRANT SELECT ON SOURCE\_SCHEMA.\* to CustomUser;

GRANT TRIGGER ON SOURCE\_SCHEMA.\* TO CustomUser;

Also on MySQL databases, you can get the following error: “You do not have the SUPER privilege and binary logging is enabled \(you might want to use the less safe log\_bin\_trust\_function\_creators variable\)“. To solve this, the user must have the SUPER privilege, or you can set the global log\_bin\_trust\_function\_creators to 1 with: SET GLOBAL log\_bin\_trust\_function\_creators = 1.

</td>
</tr>
<tr>
<td valign="top">

MSSQL

</td>
<td valign="top">

Users must have CREATE TABLE, CREATE PROCEDURE, and CREATE VIEW privileges on the database and ALTER on the schema. To use CREATE TRIGGER, users must have ALTER privileges on the table or in the original schema. You can grant the necessary SELECT, INSERT, UPDATE, ALTER, EXECUTE, CREATE SEQUENCE privileges to user CustomUser in the schema CUSTOM\_SCHEMA or, alternatively, you can use the CONTROL privilege to provide the necessary privileges in schema CUSTOM\_SCHEMA. The SQL statements needed to run the example are:

GRANT SELECT, INSERT, UPDATE, ALTER, EXECUTE, CREATE SEQUENCE on schema :: CUSTOM\_SCHEMA to CustomUser;

GRANT CONTROL ON SCHEMA :: CUSTOM\_SCHEMA TO CustomUser;

GRANT SELECT ON SCHEMA :: SOURCE\_SCHEMA TO CustomUser;

GRANT ALTER ON SCHEMA :: SOURCE\_SCHEMA TO CustomUser;

GRANT CREATE TABLE to CustomUser;

GRANT CREATE PROCEDURE to CustomUser;

GRANT CREATE VIEW to CustomUser.

</td>
</tr>
<tr>
<td valign="top">

Azure SQL

</td>
<td valign="top">

The SQL statements are the same as for MSSQL.

</td>
</tr>
<tr>
<td valign="top">

Oracle

</td>
<td valign="top">

The objects in Oracle don’t belong to a schema, they have an owner. In this example, we have a user ‘CustomUser’, a schema ‘CustomUser’, and the SOURCE table in schema ‘SOURCE’ which belongs to the user ‘SOURCE’. We can’t assign privileges to an entire schema on Oracle, so the user ‘CustomUser’ must have the SELECT privilege on the table SOURCE. The user ‘CustomUser’ also needs CREATE TABLE, CREATE VIEW, CREATE SEQUENCE, and CREATE PROCEDURE privileges, because these privileges are not over a schema. The owner of the TRIGGER privilege on the referenced objects is the user who runs it. Triggers for INSERT, DELETE, and UPDATE privileges reference a sequence \(\_SEQ, which is created on the custom schema ‘CustomUser’\) and the shadow table \(\_SHA\). The TRIGGER owner must have the SELECT privilege on the sequence and SELECT and INSERT privileges on the shadow table. These objects are created when the Table Replicator operator initializes. Give the needed privileges before initialization by assigning SELECT ANY SEQUENCE, SELECT ANY TABLE, and INSERT ANY TABLE to the owner \(which in the example is the user S\). Configure the custom schema by using these SQL statements:

GRANT CREATE SESSION TO SOURCE;

GRANT SELECT ANY SEQUENCE TO SOURCE;

GRANT SELECT ANY TABLE TO SOURCE;

GRANT INSERT ANY TABLE TO SOURCE;

GRANT CREATE SESSION TO CustomUser;

GRANT SELECT ON SOURCE.SOURCE TO CustomUser;

GRANT CREATE ANY TRIGGER TO CustomUser;

GRANT CREATE VIEW TO CustomUser;

GRANT CREATE SEQUENCE TO CustomUser;

GRANT CREATE PROCEDURE TO CustomUser;

GRANT CREATE TABLE TO CustomUser;

GRANT DROP ANY PROCEDURE TO CustomUser;

GRANT DROP ANY VIEW TO CustomUser;

GRANT DROP ANY SEQUENCE TO CustomUser;

GRANT DROP ANY TABLE TO CustomUser;

GRANT DROP ANY TRIGGER TO CustomUser.

</td>
</tr>
</table>

