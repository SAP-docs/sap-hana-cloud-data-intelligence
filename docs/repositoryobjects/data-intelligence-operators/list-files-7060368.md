<!-- loio706036857e674d1cad185b49d66b664b -->

# List Files

This operator lists files and directories from various storage services, which are identified by a File Reference, for example, a pair of connection and path \(qualified name\) values.



Supported services are:

-   [Alibaba Cloud Object Storage Service (OSS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/6b7c7eb2a990471fb604025327b9fd25.html "Many of the SAP Data Intelligence storage operators support the Alibaba Cloud OSS, and there are common characteristics that this service has across the operators.") :arrow_upper_right:
-   [Amazon Simple Storage Service (AWS S3)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/959ed43201ba4ef082016cb10e4ade6d.html "Many of the SAP Data Intelligence connectors support AWS S3, and there are common characteristics that this service has across the operators.") :arrow_upper_right: \(also supporting S3-compatible services\)
-   [Google Cloud Storage (GCS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/bd88d109721146a684cb47462864ccde.html "GCS is Google's Object Storage cloud service. Additional information, including the documentation, can be found at the official GCS Homepage.") :arrow_upper_right:
-   [Hadoop Distributed File System (HDFS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/d77575d3b41f41ef8eee5ade46ff7d84.html "Hadoop Distributed File System is Apache's distributed storage solution. For more information, see the official HDFS documentation.") :arrow_upper_right:
-   HANA Data Lake \(HDL\_FILES\)
-   [Microsoft Azure Data Lake (ADL)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/e78850b420ec41728036e6bc01f4535f.html "Azure Data Lake (ADL) is Microsoft's Data Lake cloud storage service. Additional information, including the documentation, can be found at the official ADL Homepage.") :arrow_upper_right:
-   Microsoft Azure Data Lake Gen. 2 \(ADL\_V2\)
-   [Microsoft Azure Blob Storage (WASB)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/5ecd01cac1524edba05aa4a262e3eeac.html "Azure Storage Blob (WASB) is one of Microsoft's cloud storage services. Additional information, including the documentation, can be found at the official WASB homepage.") :arrow_upper_right:
-   [SDL (Semantic Data Lake)](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/a6b555f56d8c4641bd1a248231202050.html "The SDL connection type connects to and accesses information from remote object stores.") :arrow_upper_right:
-   SSH File Transfer Protocol \(SFTP\)

A `List` operation is triggered according to its configuration. Check the parameter `List` for further information.



<a name="loio706036857e674d1cad185b49d66b664b__section_qdh_d3k_cjb"/>

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

List

</td>
<td valign="top">

mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The operation mode. Details of each mode are detailed below.

Accepted values:

-   **On input**: A file is read for every reference input received. If the reference is a directory, nothing is done and no output is produced.

-   **Once**: The file pointed by the operator configuration parameters is read once as soon as the graph is running.

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

Points to the static connection to list from. Only available if *List* is set to `Once`.

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

Points to the dynamic connection to list from. The connection configuration is detailed here. It uses the file connection attribute. Only available if *List* is set to `On input`.

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

Only available if List is set to Once. Points to the qualified name used in the File Reference. Must follow the qualified name encoding standard. When the Connection is set, the UI file browsing may be used to set this parameter's value.

Default: /

</td>
</tr>
<tr>
<td valign="top">

Recursive

</td>
<td valign="top">

recursive

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Whether to browse through subdirectories recursively. If false, only the files and directories at the first level of the requested path are listed.

Default: false

</td>
</tr>
<tr>
<td valign="top">

List Directories

</td>
<td valign="top">

listDirectories

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Whether to list directories. If false, only files are listed, otherwise, both are listed.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Filter

</td>
<td valign="top">

filter

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Sets a specific filter for outputs.

Accepted values:

-   **None**: no filter is used, all outputs occur normally.

-   **With regular expression**: only names that match the regular expression specific in Pattern are sent as output.


Default: "None"

</td>
</tr>
<tr>
<td valign="top">

Pattern

</td>
<td valign="top">

pattern

</td>
<td valign="top">

string

</td>
<td valign="top">

The regular expression used to filter outputs. Only names that match the expression are sent as output. It uses the RE2 standard [https://github.com/google/re2/wiki/Syntax](https://github.com/google/re2/wiki/Syntax)

Default: ""

</td>
</tr>
</table>



<a name="loio706036857e674d1cad185b49d66b664b__section_knq_5f3_vdb"/>

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

The File Reference pointing to the directory to be listed. If it points to a file, the input is replicated to the output.

</td>
</tr>
</table>



<a name="loio706036857e674d1cad185b49d66b664b__section_swc_cg3_vdb"/>

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

ref

</td>
<td valign="top">

message.fileReference

</td>
<td valign="top">

The File Reference pointing to one file or directory resulting from the list operation. It contains the standard set of batching attributes, except for the optional message.batchCount, regarding a single operation.

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

