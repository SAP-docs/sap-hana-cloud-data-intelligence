<!-- loio605e08a3eca2402c9495b2f50781a779 -->

# Structured File Producer V3

Structured File Producer operator reads from any table input and produces a file \(CSV, ORC, or Apache Parquet\) in the specified storage. This operator is supported in Generation 2 graphs.



> ### Caution:  
> Support for Microsoft Azure Data Lake Storage Gen1 \(ADL\) in this operator is deprecated.



The supported cloud storages include the following:

-   Microsoft Azure Data Lake Storage V2 \(ADL\_V2\)
-   Google Cloud Storage \(GCS\)
-   Hadoop Distributed File System \(HDFS\)
-   Alibaba Cloud Object Storage Service \(OSS\)
-   Amazon Simple Storage Service \(S3\)
-   Semantic Data Lake \(SDL\)
-   Microsoft Azure Storage Blob \(WASB\)

> ### Note:  
> This operator produces runtime metrics. See [Operator Metrics](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/994bc115589d40929905dc401263ab10.html "The operators publish a set of metrics as soon as the graph is executed. Each operator provides a different set of metrics.") :arrow_upper_right:.



<a name="loio605e08a3eca2402c9495b2f50781a779__section_sq1_nf3_vdb"/>

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

The storage in which the file is written.

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
<tr>
<td valign="top">

Mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Defines the write mode for CSV files. Options are Overwrite and Append. Overwrite replaces the existing content, while Append adds data to an existing file. In both cases, if the file does not exist yet, it is created during the writing process. Important: GCS, S3, and WASB do not allow append.

</td>
</tr>
<tr>
<td valign="top">

Format

</td>
<td valign="top">

string

</td>
<td valign="top">

The supported cloud storage output file formats include CSV, PARQUET, and ORC. The CSV file conforms to the RFC-4180 specification, where the row delimiter is always CRLF and the escape character is always double-quotes.

</td>
</tr>
<tr>
<td valign="top">

CSV Properties

</td>
<td valign="top">

object

</td>
<td valign="top">

Properties of the CSV output.

-   Column delimiter \(optional\): The field separator. These characters are supported: , ; | : TAB.
-   Header Included \(optional\): Indicates whether each CSV output has a header as the first line.



</td>
</tr>
<tr>
<td valign="top">

Additional Properties

</td>
<td valign="top">

object

</td>
<td valign="top">

Additional properties related to the upload options to cloud storage. It is only applicable when a cloud storage service is selected.

-   Compression type: Compression type used when uploading file into cloud service.



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

Write part files

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Defines whether the writer produces a single file or a directory of files.

</td>
</tr>
<tr>
<td valign="top">

Limit part file records

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Defines whether to limit individual partition files with a maximum number of records.

</td>
</tr>
<tr>
<td valign="top">

Max part file records

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the maximum number of records in each partition file. This guarantees that partition files will not exceed this number.

</td>
</tr>
<tr>
<td valign="top">

Part file write mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Defines the write mode for partition files. Options are Overwrite and Append. Overwrite deletes the existing directory if it was a partition file directory and re-create it. Append adds new files to an existing partition file directory. Important: If appending, the producer must match the existing format of the partition file directory, including the format and column layout.

</td>
</tr>
</table>



<a name="loio605e08a3eca2402c9495b2f50781a779__section_p1s_jy5_fnb"/>

## Placeholders

For file names, we support the following placeholders:

-   <sourceTableName\>: When connected to a table consumer, this placeholder is replaced by the table name of the source. For SQL consumers, this placeholder is replaced by SQL\_Table.

    > ### Note:  
    > Unsupported characters \(anything besides alphanumeric characters, a hyphen, and a period\) are replaced with an underscore.

-   <counter\>: An incremental integer for each file written, starting with 1.
-   <date\>: The date at the moment of writing, in the format yyyyMMdd.
-   <time\>: The time at the moment of the writing, in the format HHmmss.
-   <timestamp\>: The timestamp at the moment of the writing, in the format yyyyMMdd\_HHmmss.
-   <partitionName\>: The partition number if the consumer has partitions. For example, 0, 1, and so on. Important: If the consumer has partitions, and the number is not specified, the partition number is always appended to the file name to avoid concurrency issues during writing.

> ### Note:  
> Data preview does not work in the custom editor while using placeholders because the file names are dynamically generated during runtime.



<a name="loio605e08a3eca2402c9495b2f50781a779__section_rl3_wy5_fnb"/>

## Remote File Name Conventions

Each cloud provider has its own naming convention for defining bucket and object names. Follow these conventions to avoid any source-related issue.

Even though operators accept most special characters, we recommend that only alphanumeric characters are used. Using alphanumeric characters avoids any undesired issues because all sources work well with such characters. Furthermore, some special characters such as ", +, and, are not allowed by the Flowagent File Producer operator and should not be used.



<a name="loio605e08a3eca2402c9495b2f50781a779__section_knq_5f3_vdb"/>

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



<a name="loio605e08a3eca2402c9495b2f50781a779__section_swc_cg3_vdb"/>

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

Outputs a scalar containing the name of the object that was written.

</td>
</tr>
</table>

