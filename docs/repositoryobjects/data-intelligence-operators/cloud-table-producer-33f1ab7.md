<!-- loio33f1ab78d60c47d0bcda46629af55038 -->

# Cloud Table Producer

The Cloud Table Producer operator reads from any table input and produces a table in the specified database.



Supported databases and staging locations including the following:

-   Google BigQuery \(GCP\_BIGQUERY\)
    -   Google Cloud Storage \(GCS\). Note that both connections have to be under the same project.

-   Snowflake \(SNOWFLAKE\)
    -   Amazon Simple Storage Service \(S3\) and Microsoft Azure Storage Blob \(WASB\)


You can load data to the selected target:

1.  The source data is loaded to a staging service supported by the target.
2.  A load command is issued to load the data from the staging location to the target.
3.  The staging file is deleted from the staging location.

This operator requires a staging connection to load data to the target. All staged files are removed after loading is complete. This operator produces runtime metrics. To learn more, see [Operator Metrics](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/994bc115589d40929905dc401263ab10.html "The operators publish a set of metrics as soon as the graph is executed. Each operator provides a different set of metrics.") :arrow_upper_right:. The metrics refer to the staging part of the load. There aren’t any metrics for the load from the staging area to the database because it is run by the target database.

It is important to properly map data types to the target table because cloud databases do not support CLOB data types.

This operator supports resiliency when used with Structured Data Operators \(Flowagent operators\) with source partitions. However, it does not support resiliency when used with other consumer operators like ABAP readers.

> ### Caution:  
> Pause/Resume functionality does not work with this operator and could result in data loss.



<a name="loio33f1ab78d60c47d0bcda46629af55038__section_dyj_m45_fnb"/>

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

String

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

Object

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

Object

</td>
<td valign="top">

Remote dataset of the selected target object.

</td>
</tr>
<tr>
<td valign="top">

Staging Connection ID

</td>
<td valign="top">

Object

</td>
<td valign="top">

Connection ID of the staging cloud storage.

</td>
</tr>
<tr>
<td valign="top">

Staging Path

</td>
<td valign="top">

String

</td>
<td valign="top">

Path where the staging data is temporarily written.

</td>
</tr>
<tr>
<td valign="top">

Mode

</td>
<td valign="top">

String

</td>
<td valign="top">

Write mode.

-   Append: Add data to an existing table.
-   Truncate: Clear the table before inserting data.



</td>
</tr>
<tr>
<td valign="top">

Maximum Batch Size

</td>
<td valign="top">

Integer

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

Boolean

</td>
<td valign="top">

Set to True when the automatic calculation does not provide optimal performance. When set to True, each batch of records contains the number of records entered in the Maximum Batch Size option. For example, when Maximum Batch Size is set to 1000, and Use Defined Batch Size is set to True, then there are 1000 records in each batch. When set to False, then each batch is between 10 and 1000 rows.

</td>
</tr>
</table>



<a name="loio33f1ab78d60c47d0bcda46629af55038__section_pty_hm5_fnb"/>

## Input


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

inTable

</td>
<td valign="top">

Table

</td>
<td valign="top">

Table type port that can be connected to other operators producing table types, such as other structured operators.

</td>
</tr>
</table>



<a name="loio33f1ab78d60c47d0bcda46629af55038__section_p31_rm5_fnb"/>

## Output


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

out

</td>
<td valign="top">

Scalar

</td>
<td valign="top">

Outputs a scalar containing the name of the object that was written.

Output headers:

-   com.sap.headers.producer
-   com.sap.headers.partition \(if consumer is configured with partition\)



</td>
</tr>
</table>

