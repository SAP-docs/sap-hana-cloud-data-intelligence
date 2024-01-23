<!-- loio9958a659e47541849b47bd07a4b0a171 -->

# Flowagent SQL Executor V2

Performs an SQL Statement to any supported database. Supported in Generation 2 graphs.



It uses Flowagent subengine to connect to the database. The specific SQL syntax depends on the specified database.

It provides a way to run SQL commands such as `CREATE`, `INSERT`, `DELETE`, and `UPDATE` in the database source. Multiple commands can be provided, where they must be separated by a specified separator \(default is ;\). The output will be success if the commands were successfully run in the source. If a command fails, it throws an error, which the outError port catches, if it is mapped.

> ### Note:  
> This operator is not suitable for data ingestion use cases even though commands such as INSERT and UPDATE are supported. Sending multiple batches of input statements results in poor operator performance.



The supported databases are:

-   Azure SQL DB \(AZURE\_SQL\_DB\)
-   DB2 Database \(DB2\)
-   SAP HANA Database \(HANA\)
-   SAP HANA Data Lake Database \(HDL\_DB\)
-   Microsoft SQL Server \(MSSQL\)
-   MySQL Database \(MYSQL\)
-   Oracle Database OSS \(ORACLE\)
-   Redshift Database \(REDSHIFT\)
-   SAP IQ Database \(SAP\_IQ\)
-   Snowflake Database \(SNOWFLAKE\)
-   Teradata Database \(TERADATA\)
-   Google BigQuery \(GCP\_BIGQUERY\)



<a name="loio9958a659e47541849b47bd07a4b0a171__section_sq1_nf3_vdb"/>

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

Connection ID

</td>
<td valign="top">

serviceConnection

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

SQL Statement\(s\)

</td>
<td valign="top">

sqlStatements

</td>
<td valign="top">

string

</td>
<td valign="top">

SQL statement\(s\) that are standard to the source. Statements must be separated by a specified separator.

</td>
</tr>
<tr>
<td valign="top">

Separator

</td>
<td valign="top">

separator

</td>
<td valign="top">

string

</td>
<td valign="top">

Separator that will be used to split the input into SQL statements.

</td>
</tr>
<tr>
<td valign="top">

Additional Session Parameters

</td>
<td valign="top">

additionalSessionParameters

</td>
<td valign="top">

string

</td>
<td valign="top">

Set session parameters that will affect the connection with the source.

</td>
</tr>
</table>



<a name="loio9958a659e47541849b47bd07a4b0a171__section_knq_5f3_vdb"/>

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

sql

</td>
<td valign="top">

scalar

</td>
<td valign="top">

SQL statements that are standard to the source. Statements must be separated by a defined separator.

</td>
</tr>
</table>



<a name="loio9958a659e47541849b47bd07a4b0a171__section_swc_cg3_vdb"/>

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

scalar

</td>
<td valign="top">

Output `success` if the commands were successfully processed.

</td>
</tr>
<tr>
<td valign="top">

error

</td>
<td valign="top">

structure

</td>
<td valign="top">

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

