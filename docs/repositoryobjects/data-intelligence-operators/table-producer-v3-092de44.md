<!-- loio092de44245ca462fbc150aece15e9107 -->

# Table Producer V3

The Table Producer operator reads from any table input and produces a table in the specified database. This operator is supported in Generation 2 graphs.



The supported databases include the following:

-   SAP HANA \(HANA\_DB\)
-   SAP HANA Data Lake Database \(HDL\_DB\)
-   SAP IQ \(SAP\_IQ\)

> ### Note:  
> This operator produces runtime metrics. See [Operator Metrics](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/994bc115589d40929905dc401263ab10.html "The operators publish a set of metrics as soon as the graph is executed. Each operator provides a different set of metrics.") :arrow_upper_right:.



<a name="loio092de44245ca462fbc150aece15e9107__section_sq1_nf3_vdb"/>

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

The database where the tabular data is written.

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

Connection ID of the target system.

</td>
</tr>
<tr>
<td valign="top">

Target

</td>
<td valign="top">

object

</td>
<td valign="top">

Remote dataset of the target object.

</td>
</tr>
</table>

Enter the required target table information based on the selected database type. If SAP IQ or SAP HANA Data Lake database is selected, the following property is available:


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

Bulk load error toleration

</td>
<td valign="top">

object

</td>
<td valign="top">

Define the number of rows that can have an error for each failure including: unique, null, data value, and foreign key.

-   Unique errors: Number of unique errors to be tolerated.
-   Null errors: Number of null errors to be tolerated.
-   Data value errors: Number of data value errors to be tolerated.
-   Foreign key errors: Number of foreign key operators to be tolerated.



</td>
</tr>
<tr>
<td valign="top">

Mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Write mode.

-   Append: Add data to an existing table. When append is selected, the aditional option *Update records based on primary key* is shown. When this option is selected, the records already in the table are updated if the primary key is the same as a new record being appended. This behavior is the same as using an UPSERT SQL command. If *Update records based on primary key* is not selected and a collision on the primary key happens, then an error is thrown and the graph fails.
-   Overwrite: Drop the table and create another one according to the source schema.
-   Truncate: Clear the table before inserting data.
-   Delete: Delete the records based on the input data and the column mapping provided. The data on the target that matches the mapped columns are deleted. Binary columns \(LOB\) can’t be selected in the mapping for the delete mode.



</td>
</tr>
<tr>
<td valign="top">

Maximum Batch Size

</td>
<td valign="top">

integer

</td>
<td valign="top">

The maximum number of records from the source included in each batch. The actual number of records is automatically calculated based on the dataset definition. To disable the automatic calculation, set the Use Defined Batch Size option to True.

</td>
</tr>
<tr>
<td valign="top">

Use Defined Batch Size

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Set to True when the automatic calculation doesn’t provide optimal performance. When set to True, each batch of records contains the number of records entered in the Maximum Batch Size option. For example, when Maximum Batch Size is set to 1000, and Use Defined Batch Size is set to True, then there are 1000 records in each batch. When set to False, then each batch is between 10 and 1000 rows.

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



<a name="loio092de44245ca462fbc150aece15e9107__section_rs1_qd5_4pb"/>

## Bulk Loading

Whenever possible, bulk load is enabled for improved loading performance.

-   SAP IQ: Bulk load is enabled by default for all sources unless there is a BLOB datatype in the source. If there are BLOB objects, remove them using SQL consumer operators or by creating a view in the source. If it is not possible to remove the BLOB objects, this operator loads the data via the regular loading, which might be slow. The bulk load uses a LOAD TABLE statement, relying on named pipes to transfer the data file to the target. To use the LOAD TABLE statement, the SAP IQ user must have the following permissions in the server: LOAD TABLE and ALLOW\_READ\_CLIENT\_FILE. The user might have to be the owner of the table, have database administrator authority, or have ALTER table permission to use the LOAD TABLE statement, depending on the ‘-gl’ property used to start the SAP IQ server.
-   SAP HANA Data Lake Database: Bulk load is enabled by default for all sources unless there is a BLOB datatype in the source. If there are BLOB objects, remove them using SQL consumer operators or by creating a view in the source. If it is not possible to remove the BLOB objects, this operator loads the data via the regular loading, which might be slow. The bulk load uses a LOAD TABLE statement, relying on named pipes to transfer the data file to the target. To use the LOAD TABLE statement, the HDL DB user must have the following permissions in the server: LOAD TABLE and ALLOW\_READ\_CLIENT\_FILE. The user might have to be the owner of the table, have database administrator authority, or have ALTER table permission to use the LOAD TABLE statement.



<a name="loio092de44245ca462fbc150aece15e9107__section_knq_5f3_vdb"/>

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

inTable

</td>
<td valign="top">

table

</td>
<td valign="top">

Table type port which can be connected to other operators producing table types, such as other structured operators.

</td>
</tr>
</table>



<a name="loio092de44245ca462fbc150aece15e9107__section_swc_cg3_vdb"/>

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

out

</td>
<td valign="top">

scalar

</td>
<td valign="top">

Outputs a scalar containing the name of the object that was written:

</td>
</tr>
</table>

This operator supports resiliency when used with structured consumers \(Flowagent operators\) with source partitions. However, it does not support resiliency when used with other consumer operators like ABAP readers.

> ### Caution:  
> Pause/Resume functionality does not work with this operator and could result in data loss.

