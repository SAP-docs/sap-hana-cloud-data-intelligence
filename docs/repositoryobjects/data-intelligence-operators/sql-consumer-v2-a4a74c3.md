<!-- loioa4a74c394c874270a285df3eb5d4daca -->

# SQL Consumer V2

SQL Consumer operator reads from a specified database using native SQL. Supported in Generation 2 graphs.



The operator produces a table output and you can connect to any other operator that consumes table data, such as operators from the Structured Operators category. For example, [Data Transform V2](data-transform-v2-a415f61.md) or [Structured File Producer V3](structured-file-producer-v3-605e08a.md).

The supported databases are:

-   Azure SQL DB \(AZURE\_SQL\_DB\)
-   DB2 Database \(DB2\)
-   Google BigQuery SQL \(GCP\_BIGQUERY\)
-   SAP HANA \(HANA\_DB\)
-   SAP HANA Data Lake Database \(HDL\_DB\)
-   Microsoft SQL Server \(MSSQL\)
-   MySQL Database \(MYSQL\)
-   Oracle Database OSS \(ORACLE\)
-   Redshift Database \(REDSHIFT\)
-   SAP IQ Database \(SAP\_IQ\)
-   Snowflake Database \(SNOWFLAKE\)
-   Teradata Database \(TERADATA\)

> ### Note:  
> This operator produces runtime metrics. See [Operator Metrics](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/994bc115589d40929905dc401263ab10.html "The operators publish a set of metrics as soon as the graph is executed. Each operator provides a different set of metrics.") :arrow_upper_right:



<a name="loioa4a74c394c874270a285df3eb5d4daca__section_sq1_nf3_vdb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Parameter

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

Service

</td>
<td valign="top">

string

</td>
<td valign="top">

The database from where to consume tabular data.

</td>
</tr>
<tr>
<td valign="top">

Connection ID

</td>
<td valign="top">

object

</td>
<td valign="top">

Connection ID of the source system.

</td>
</tr>
<tr>
<td valign="top">

Native SQL Statement

</td>
<td valign="top">

string

</td>
<td valign="top">

SQL statement used to read from the source. The syntax depends on the underlying source.

</td>
</tr>
<tr>
<td valign="top">

Partition Type

</td>
<td valign="top">

string

</td>
<td valign="top">

Partitioning is used to enable data reading in parallel. In this case, the consumer and producer must be inside a group with multiplicity equal to the number of partitions.

> ### Note:  
> Partition is not supported when this consumer operator is combined with the Data Transform operator.



</td>
</tr>
<tr>
<td valign="top">

Logical Partition Specification

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

Additional Session Parameters

</td>
<td valign="top">

string

</td>
<td valign="top">

Set session parameters that affect the connection with the source.

</td>
</tr>
<tr>
<td valign="top">

Maximum Fetch Size

</td>
<td valign="top">

integer

</td>
<td valign="top">

The maximum number of records from the source included in each batch. The actual number of records is automatically calculated based on the dataset definition. To disable the automatic calculation, set the *Use Defined Fetch Size* option to True.

</td>
</tr>
<tr>
<td valign="top">

Use Defined Fetch Size

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Set to True when the automatic calculation doesn’t provide optimal performance. When set to True, each batch of records contains the number of records entered in the *Maximum Fetch Size* option. For example, when *Maximum Fetch Size* is set to 1000, and *Use Defined Fetch Size* is set to True, then there are 1000 records in each batch. When set to False, then each batch is between 10 and 1000 rows.

</td>
</tr>
<tr>
<td valign="top">

Enable ODBC Tracing

</td>
<td valign="top">

boolean

</td>
<td valign="top">

This property defines whether the ODBC logs are produced. When set to False, there are no changes in the graph processing or generated logs. When set to True, ODBC logs are written in a new log file that can be used for troubleshooting purposes.

> ### Note:  
> This option is available for the SAP HANA connection type.
> 
> Setting this option to True causes a negative performance impact and should only be used for troubleshooting purposes.

Default: false

</td>
</tr>
</table>



<a name="loioa4a74c394c874270a285df3eb5d4daca__section_oyd_qrz_2pb"/>

## Custom Editor

This operator uses a custom editor user interface. For details, see [Custom Editor](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/8cda7c3a4ab74c86ba5752456418c4b0.html "Use the Custom Editor to update the source dataset and projection and filters are pushed down to the source.") :arrow_upper_right:.



<a name="loioa4a74c394c874270a285df3eb5d4daca__section_knq_5f3_vdb"/>

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

scalar

</td>
<td valign="top">

Trigger to indicate that the operator should start processing.

> ### Note:  
> The input port is optional. If the input port does not have a connection, then the operator starts when the graph starts running.



</td>
</tr>
</table>



<a name="loioa4a74c394c874270a285df3eb5d4daca__section_swc_cg3_vdb"/>

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

outTable

</td>
<td valign="top">

table

</td>
<td valign="top">

Table type port, which can be used to connect to other operators consuming table types, such as other structured operators.

</td>
</tr>
</table>

