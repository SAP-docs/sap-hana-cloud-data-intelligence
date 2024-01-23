<!-- loiob4e99539ba6d422e849cf9e8147dfd6d -->

# Table Producer V1 \(Deprecated\)

This operator reads from any structured operators and produces a table in the specified database. Previously supported in Generation 1 graphs.



The supported databases are:

-   SAP HANA
-   SAP IQ

> ### Note:  
> This operator produces runtime metrics. See [Operator Metrics](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/994bc115589d40929905dc401263ab10.html "The operators publish a set of metrics as soon as the graph is executed. Each operator provides a different set of metrics.") :arrow_upper_right:



<a name="loiob4e99539ba6d422e849cf9e8147dfd6d__section_sq1_nf3_vdb"/>

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

Database Type

</td>
<td valign="top">

string

</td>
<td valign="top">

The target database to operate. Additional parameters may depend on the selected option.

</td>
</tr>
<tr>
<td valign="top">

Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Object containing the connection parameters.

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

The table where the data is written. This field accepts two input formats: adapted dataset of the table, which can be selected via the browsing action, or qualified name in <Schema\>.<TableName\> format.

</td>
</tr>
</table>

Enter the required target table information based on the selected database type. If SAP IQ database is selected, the following properties are available:


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
</table>



<a name="loiob4e99539ba6d422e849cf9e8147dfd6d__section_yzq_rsq_prb"/>

## Delta Processing

Change Data Applier mode is only applicable to operators that support DELTA extraction, like ABAP ODP Consumer, Cloud Data Integration Consumer, and so on.

Change Data Applier Mode: The delta record provides a row type like Insert \(I\), Update \(U\), Delete \(D\), Before Image \(B\), Unknown \(X\), and so on. Either decide to keep a history of changed records \(Track Change History\), or decide to apply the changes directly to the target \(Apply Change Data\). Currently, only HANA database supports Apply Change Data mode.



<a name="loiob4e99539ba6d422e849cf9e8147dfd6d__section_rs1_qd5_4pb"/>

## Bulk Loading

Whenever possible, bulk load is enabled for improved loading performance.

SAP IQ: Bulk load is enabled by default for all sources unless there is a BLOB datatype in the source. If there are BLOB objects, remove them using SQL consumer operators or by creating a view in the source. If it is not possible to remove the BLOB objects, this operator loads the data via the regular loading, which might be slow. The bulk load uses a LOAD TABLE statement, relying on named pipes to transfer the data file to the target. To use the LOAD TABLE statement, the SAP IQ user must have the following permissions in the server: LOAD TABLE and ALLOW\_READ\_CLIENT\_FILE. The user might have to be the owner of the table, have database administrator authority, or have ALTER table permission to use the LOAD TABLE statement, depending on the ‘-gl’ property used to start the SAP IQ server.



<a name="loiob4e99539ba6d422e849cf9e8147dfd6d__section_znw_wsq_prb"/>

## Unknown Datatypes

When a column has the Unknown datatype, it is skipped during processing, and it is not be reflected in the target table. To avoid this behavior, it is necessary to override the unknown datatype in the adapted dataset of the consumer. See the example below where $\{user-defined-length\} needs to be replaced with the maximum length of the COL0 in the dataset:

-   Original metadata

    > ### Sample Code:  
    > ```
    > "adapted_dataset": {
    > "schema": {
    >     "tableBasedRepresentation": {
    >         "attributes": [
    >             {
    >                 "name": "COL0",
    >                 "datatype": "UNKNOWN",
    >                 "nativeDatatype": "XML"
    >             }
    >         ]
    >     }
    > }
    > }
    > ```

-   Modified metadata

    > ### Sample Code:  
    > ```
    > "adapted_dataset": {
    > "schema": {
    >     "tableBasedRepresentation": {
    >         "attributes": [
    >             {
    >                 "name": "COL0",
    >                 "datatype": "STRING",
    >                 "length": ${user-defined-length},
    >                 "nativeDatatype": "XML"
    >             }
    >         ]
    >     }
    > }
    > }
    > ```




<a name="loiob4e99539ba6d422e849cf9e8147dfd6d__section_knq_5f3_vdb"/>

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

Table type port, which comes as output from other structured operators.

</td>
</tr>
</table>



<a name="loiob4e99539ba6d422e849cf9e8147dfd6d__section_swc_cg3_vdb"/>

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

outMessage

</td>
<td valign="top">

message

</td>
<td valign="top">

Outputs a message object with the following definition:

-   Body: The fully qualified name of the target table.
-   Attributes:
    -   producer.totalRows: Number of rows written to the target.
    -   producer.type: Type of the producer that generated the message. Depending on which operator generated the message, you could see: CSV for Flowagent CSV Producer, File for Flowagent File Producer, or Table for Flowagent Table Producer.
    -   producer.subType: Subtype of the object that was generated in the target. Depending on the producer settings, you could see one of the following:: TABLE, CSV, PARQUET, or ORC depending on the producer settings.
    -   producer.partition.count: Number of partitions from the source.
    -   producer.partition.index: The partition index that was processed. The index ranges from 0 to partition.count.

-   Encoding: string



</td>
</tr>
</table>

