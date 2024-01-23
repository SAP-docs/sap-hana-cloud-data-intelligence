<!-- loio847395d376ed428386764577108fbf8b -->

# SQL Consumer V1 \(Deprecated\)

SQL Consumer operator reads from a specified database using native SQL. Previously supported in Generation 1 graphs.



This operator produces a structured output, and you need to connect it to other operators from Structured Data Operators category.

The supported databases are:

-   Azure SQL DB \(AZURE\_SQL\_DB\)
-   DB2 Database \(DB2\)
-   Google BigQuery SQL \(GBQ\)
-   SAP HANA \(HANA\_DB\)
-   Microsoft SQL Server \(MSSQL\)
-   MySQL Database \(MYSQL\)
-   Oracle Database OSS \(ORACLE\)
-   Redshift Database \(REDSHIFT\)
-   SAP IQ Database \(SAP\_IQ\)

> ### Note:  
> This operator produces runtime metrics. See [Operator Metrics](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/994bc115589d40929905dc401263ab10.html "The operators publish a set of metrics as soon as the graph is executed. Each operator provides a different set of metrics.") :arrow_upper_right:.



<a name="loio847395d376ed428386764577108fbf8b__section_sq1_nf3_vdb"/>

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

Database type

</td>
<td valign="top">

string

</td>
<td valign="top">

Database on which the SQL statements are executed. Supported databases are displayed below.

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

Native SQL

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
</table>



<a name="loio847395d376ed428386764577108fbf8b__section_knq_5f3_vdb"/>

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

Trigger to indicate that the operator should start processing.

> ### Note:  
> The input port is optional. If the input port does not have a connection, then the operator starts when the graph starts running.



</td>
</tr>
</table>



<a name="loio847395d376ed428386764577108fbf8b__section_swc_cg3_vdb"/>

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

Table type port, which can be used to connect to other structured operators.

</td>
</tr>
</table>

