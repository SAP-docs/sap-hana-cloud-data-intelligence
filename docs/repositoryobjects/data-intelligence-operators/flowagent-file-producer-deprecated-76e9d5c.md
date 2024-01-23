<!-- loio76e9d5c257b646f9825b06d238b50bb6 -->

# Flowagent File Producer \(Deprecated\)

The Flowagent File Producer reads from any Flowagent-based consumer operator and produces a file. The location of the file depends on specified storage type \(local and cloud\). The format of the file will be CSV, where the CSV properties can be specified in the CSV Properties.



This operator is deprecated. We recommend using the [Structured File Producer V3](structured-file-producer-v3-605e08a.md) operator.

> ### Caution:  
> Support for Microsoft Azure Data Lake Storage Gen1 \(ADL\) in this operator is deprecated.



<a name="loio76e9d5c257b646f9825b06d238b50bb6__section_sq1_nf3_vdb"/>

## Configuration Parameters

> ### Restriction:  
> LZO compression is not supported for Parquet files.


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

Storage Type

</td>
<td valign="top">

service

</td>
<td valign="top">

string

</td>
<td valign="top">

Optional. The storage in which the file will be written. Additional properties depend on the selected storage.

</td>
</tr>
<tr>
<td valign="top">

ADL Connection

</td>
<td valign="top">

adlConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Supported cloud storage. The object containing the connection parameters to a ADL remote.

</td>
</tr>
<tr>
<td valign="top">

GCS Connection

</td>
<td valign="top">

gcsConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Supported cloud storage. The object containing the connection parameters to a GCS remote.

</td>
</tr>
<tr>
<td valign="top">

HDFS Connection

</td>
<td valign="top">

hdfsConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Supported cloud storage. The object containing the connection parameters to a HDFS remote.

</td>
</tr>
<tr>
<td valign="top">

HDL FILES Connection

</td>
<td valign="top">

hdl\_filesConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Optional. Object containing the connection parameters to a HDL FILES storage.

</td>
</tr>
<tr>
<td valign="top">

S3 Connection

</td>
<td valign="top">

s3Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Supported cloud storage. The object containing the connection parameters to a S3 remote.

</td>
</tr>
<tr>
<td valign="top">

WASB Connection

</td>
<td valign="top">

wasbConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Supported cloud storage. The object containing the connection parameters to a WASB remote.

</td>
</tr>
<tr>
<td valign="top">

SDL Connection

</td>
<td valign="top">

sdlConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Supported cloud storage. Connection to SAP-provided data lake.

</td>
</tr>
<tr>
<td valign="top">

HDL FILES File Name

</td>
<td valign="top">

hdl\_filesTargetObjectName

</td>
<td valign="top">

string

</td>
<td valign="top">

Optional. File path to be saved on HDL\_FILES.

</td>
</tr>
<tr>
<td valign="top">

Local File Name

</td>
<td valign="top">

path

</td>
<td valign="top">

string

</td>
<td valign="top">

A formatted string describing the output path and file name. If the root directory of the file is not provided, `"/vrep/"` will be used as default root directory of the file.

Default: `"/vrep/<sourceTableName>_<timestamp>.csv"` - only applies when storage type is local.

</td>
</tr>
<tr>
<td valign="top">

Cloud Storage File Name

</td>
<td valign="top">

 

</td>
<td valign="top">

string

</td>
<td valign="top">

Only applies when Storage type is cloud storages. File path to be saved on cloud storage.

</td>
</tr>
<tr>
<td valign="top">

Remote File Name \(Deprecated\)

</td>
<td valign="top">

targetObjectName

</td>
<td valign="top">

string

</td>
<td valign="top">

Only applies when Storage type is cloud storages. File path to be saved on cloud storage.

> ### Restriction:  
> Deprecated: Use cloud storage file name instead.

Default: `"<sourceTableName>_<timestamp>.csv"`

</td>
</tr>
<tr>
<td valign="top">

Mode

</td>
<td valign="top">

mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Defines the write mode, where overwrite will overwrite an existing file and append will append to an existing file. In both cases, if the file does not exist yet, it will be created during the write.

> ### Note:  
> Important: Google Cloud Services \(GCS\), Amazon Simple Storage Service \(S3\), and, Microsoft Azure Storage Blob \(WASB\) do not allow append.

Default: `"overwrite"`

</td>
</tr>
<tr>
<td valign="top">

Format

</td>
<td valign="top">

format

</td>
<td valign="top">

string

</td>
<td valign="top">

Output file format: CSV, Parquet, and ORC are supported for the cloud storages. The CSV that is produced conforms to the RFC-4180 specification, where the row delimiter is always CRLF and the escape character is always double quotes. Currently, only CSV is supported for local storage.

Default: `"CSV"`

</td>
</tr>
<tr>
<td valign="top">

CSV Properties

</td>
<td valign="top">

additionalProperties\_csv

</td>
<td valign="top">

object

</td>
<td valign="top">

Properties of the CSV output.

</td>
</tr>
<tr>
<td valign="top">

Column Delimiter

</td>
<td valign="top">

columnDelimiter

</td>
<td valign="top">

string

</td>
<td valign="top">

The field separator. Only the following characters are supported: , ; | : and TAB.

Default: `,`

</td>
</tr>
<tr>
<td valign="top">

Header Included

</td>
<td valign="top">

csvHeaderIncluded

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Indicates whether or not each CSV output will have a header as first line.

Default: `false`

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

Additional properties related to upload options to cloud storage. It is applicable only when a cloud storage service is selected.

</td>
</tr>
<tr>
<td valign="top">

Compression Type

</td>
<td valign="top">

compressionType

</td>
<td valign="top">

string

</td>
<td valign="top">

Compression type used when uploading file into cloud service. LZO compression is not supported for PARQUET files.

Default: `"None"`

</td>
</tr>
<tr>
<td valign="top">

Batch Size

</td>
<td valign="top">

batchSize

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the number of rows that will be inserted in a single commit.

Default: `1000`

</td>
</tr>
</table>



<a name="loio76e9d5c257b646f9825b06d238b50bb6__section_wtf_yfy_jjb"/>

## Placeholders

For file names, we support three placeholders:

-   `<sourceTableName>`: It will be replaced by the table name of the source, if this operator is connected to a Flowagent Table Consumer \(for example, Oracle Table Consumer\). For SQL Consumers, it will be replaced by `SQL_Table`, instead.

-   `<timestamp>`: It will be replaced by the timestamp at the moment of the writing, in the format `yyyyMMdd_HHmmss`.

-   `<partitionName>`: It will be replaced by the partition number if the consumer has partitions \(for example, 0, 1, ...\).

    > ### Note:  
    > If not specified and the consumer has partitions, the partition number will always be appended to the file name to avoid concurrency issues during the writing.




<a name="loio76e9d5c257b646f9825b06d238b50bb6__section_a1h_1gy_jjb"/>

## Remote File Name Conventions

Each cloud provider has its own naming convention for defining bucket and object names. These conventions should be followed accordingly to avoid any source-related issue.

Even though Flowagent-based operators accept most special characters, we recommend that only alphanumeric characters are used. This will avoid any undesired issue because all sources work well with such characters. Furthermore, some special characters such as ", +, and , are not allowed by our Flowagent File Producer operator and should not be used.



<a name="loio76e9d5c257b646f9825b06d238b50bb6__section_knq_5f3_vdb"/>

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

`inConfig` 

</td>
<td valign="top">

string.flowagent.config

</td>
<td valign="top">

The source connection information provided by Flowagent-based consumer operator from which data will be read.

</td>
</tr>
</table>



<a name="loio76e9d5c257b646f9825b06d238b50bb6__section_swc_cg3_vdb"/>

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

`outFileName` 

</td>
<td valign="top">

string

</td>
<td valign="top">

The path to the file to which content is written.

</td>
</tr>
<tr>
<td valign="top">

`Body` 

</td>
<td valign="top">

string

</td>
<td valign="top">

\(type: string\) The fully qualified name of the target table.

</td>
</tr>
<tr>
<td valign="top">

`Attributes` 

</td>
<td valign="top">

According to parameter

</td>
<td valign="top">

-   producer.totalRows \(type: string\): Number of rows written to the target.

-   producer.type \(type: string\): Type of the producer that generated the message, which can be one of the following depending on which operator generated the message: CSV for Flowagent CSV Producer, File for Flowagent File Producer, or Table for Flowagent Table Producer.

-   producer.subType \(type: string\): Subtype of the object that was generated in the target, which can be one of the following: TABLE, CSV, PARQUET, or ORC depending on the producer settings.

-   producer.partition.count \(type: integer\): Number of partitions from the source.

-   producer.partition.index \(type: integer\): Current partition index that was processed. This ranges from 0 to partition.count - 1.




</td>
</tr>
<tr>
<td valign="top">

`Encoding` 

</td>
<td valign="top">

string

</td>
<td valign="top">



</td>
</tr>
<tr>
<td valign="top">

`outMessage` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Outputs a message object with the definitions to follow.

</td>
</tr>
<tr>
<td valign="top">

`outError` 

</td>
<td valign="top">

string

</td>
<td valign="top">

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>



