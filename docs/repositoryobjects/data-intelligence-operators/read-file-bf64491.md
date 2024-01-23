<!-- loiobf64491925df47b0a02b396796f38493 -->

# Read File

Reads the content of files from various storage services.



A read operation happens according to the *Read* configuration. If reading **On input**, the input contains the used path. Otherwise, if reading **Once**, the path comes from the configuration.

The connection used varies with the *Connection* configuration. The *Connection type* **From input** is available only if reading **On input**. Otherwise, a static connection ID from **Connection Management** can be used.

For each opeation, the output is a file message. If *Output in Batches* is `true`, one operation may have many outputs.

The operator ignores directory inputs and produces no output. A directory input must have `file.isDir` set to `true`. Usually these inputs come from another operator such as [List Files](list-files-7060368.md).

Supported services are:

-   [Alibaba Cloud Object Storage Service (OSS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/6b7c7eb2a990471fb604025327b9fd25.html "Many of the SAP Data Intelligence storage operators support the Alibaba Cloud OSS, and there are common characteristics that this service has across the operators.") :arrow_upper_right:
-   [Amazon Simple Storage Service (AWS S3)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/959ed43201ba4ef082016cb10e4ade6d.html "Many of the SAP Data Intelligence connectors support AWS S3, and there are common characteristics that this service has across the operators.") :arrow_upper_right: \(also supports S3-compatible services\)
-   [Google Cloud Storage (GCS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/bd88d109721146a684cb47462864ccde.html "GCS is Google's Object Storage cloud service. Additional information, including the documentation, can be found at the official GCS Homepage.") :arrow_upper_right:
-   [Hadoop Distributed File System (HDFS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/d77575d3b41f41ef8eee5ade46ff7d84.html "Hadoop Distributed File System is Apache's distributed storage solution. For more information, see the official HDFS documentation.") :arrow_upper_right:
-   HANA Data Lake \(HDL\_FILES\)
-   [Microsoft Azure Data Lake (ADL)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/e78850b420ec41728036e6bc01f4535f.html "Azure Data Lake (ADL) is Microsoft's Data Lake cloud storage service. Additional information, including the documentation, can be found at the official ADL Homepage.") :arrow_upper_right:
-   Microsoft Azure Data Lake Gen. 2 \(ADL\_V2\).

-   [Microsoft Azure Blob Storage (WASB)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/5ecd01cac1524edba05aa4a262e3eeac.html "Azure Storage Blob (WASB) is one of Microsoft's cloud storage services. Additional information, including the documentation, can be found at the official WASB homepage.") :arrow_upper_right:
-   [SDL (Semantic Data Lake)](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/a6b555f56d8c4641bd1a248231202050.html "The SDL connection type connects to and accesses information from remote object stores.") :arrow_upper_right:
-   SSH File Transfer Protocol \(SFTP\).
-   [Local File System (/file)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/9cd7952d24f648d8babedda94a0a36af.html "Many of the SAP Data Intelligence storage operators offer support for the local file system.") :arrow_upper_right: \(it does not use a Connection ID. It is the file system presented in the System Management app, only for files found in `/files/`. The usage of the `/files/` root path \(or the `/vrep` folder\) is deprecated.\)




<a name="loiobf64491925df47b0a02b396796f38493__section_qdh_d3k_cjb"/>

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

Read

</td>
<td valign="top">

mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The operation mode. Details of each mode are found below. If *Output in batches* is enabled, each read operation may produce many outputs.

Accepted values:

-   **On input**: A read operation happens for every input received. The input informs the path to read from.

-   **Once**: A single read operation happens as soon as the graph is Running. The *Path* configuration informs the path to read from.

Default: "On input"

</td>
</tr>
<tr>
<td valign="top">

Connection \(static\)

</td>
<td valign="top">

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Points to the static connection to read from. Only available if *Read* is set to **Once**.

Default: \{\}

</td>
</tr>
<tr>
<td valign="top">

Connection \(dynamic\)

</td>
<td valign="top">

dynamicConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Points to the dynamic connection to read from. It uses the file connection attribute. Only available if *Read* is set to **On input**.

Default: \{"configurationType":"From input"\}

</td>
</tr>
<tr>
<td valign="top">

Path

</td>
<td valign="top">

path

</td>
<td valign="top">

string

</td>
<td valign="top">

Points to the file to read, relative to the used connection. It must be in the qualified name format. If the *Connection* is set with a connection ID, you may use the UI file browsing to set the path. Only available if *Read* is set to **Once**.

Default: /

</td>
</tr>
<tr>
<td valign="top">

Output in Batches

</td>
<td valign="top">

outputInBatches

</td>
<td valign="top">

bool

</td>
<td valign="top">

If `true`, each output uses batching attributes and has a body limited by *Output batch size*. Also, each operation may produce many outputs.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Output Batch Size

</td>
<td valign="top">

outputBatchSize

</td>
<td valign="top">

string

</td>
<td valign="top">

The maximum number of bytes placed in each output message. The value allows metric prefixes and an optional "i" to state binary bases \(examples below\). It is useful to reduce graph latency and memory usage. Only available if *Output in batches* is set to `true`.

Example values:

-   `"1", "1B"`: 1 byte

-   `"2kb", "2KB"`: 2\*103 bytes

-   `"2kib", "2KiB"`: 2\*210 bytes

-   `"3mb", "3MB"`: 3\*106 bytes

-   `"3mib", "3MiB"`: 3\*220 bytes


Default: 1MB

</td>
</tr>
</table>



<a name="loiobf64491925df47b0a02b396796f38493__section_knq_5f3_vdb"/>

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

ref

</td>
<td valign="top">

message.fileReference

</td>
<td valign="top">

A file message pointing to the file to read. The body is ignored. If it is a directory, the operator ignores it, producing no output.

</td>
</tr>
</table>



<a name="loiobf64491925df47b0a02b396796f38493__section_swc_cg3_vdb"/>

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

file

</td>
<td valign="top">

message.file

</td>
<td valign="top">

A file message with the contents of the file in the body. The message also has the updated `connection`, `path`, and `size` values in the file attribute.

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

An Error Message, in case an error was raised during an operation.

</td>
</tr>
</table>

