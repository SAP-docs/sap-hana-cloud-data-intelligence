<!-- loio34ab7a67606749e3a10722cbabd5092c -->

# Remove File

This operator removes files and directories from various storage services.



A **remove operation** takes place at every input, using the path its attributes point to.

By default, only single files are removed. If the Remove all configuration is enabled, any directory or file is removed instead.

The connection used varies with the connection configuration. The Connection type From input is available only if reading On input. Otherwise, a static connection ID from Connection Management can be used.

At each successful removal, the input is replicated to the output. Only one output is given per input, even if several files are removed.



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



<a name="loio34ab7a67606749e3a10722cbabd5092c__section_qdh_d3k_cjb"/>

## Configuration Parameters

****


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

Connection

</td>
<td valign="top">

dynamicConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Points to the connection to remove from. By default, it uses the connection from the input header `file.connection`.

Default: \{"configurationType":"From input"\}

</td>
</tr>
<tr>
<td valign="top">

Remove All

</td>
<td valign="top">

removeAll

</td>
<td valign="top">

bool

</td>
<td valign="top">

If set to `true`, any file or directory in the requested path is removed. Otherwise, only single files are removed, resulting in an error if the requested path points to a directory.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Ignore If Not Found

</td>
<td valign="top">

ignoreNotFound

</td>
<td valign="top">

bool

</td>
<td valign="top">

If set to `true`, any file or directory not found is ignored, instead of raising an error.

Default: false

</td>
</tr>
</table>



<a name="loio34ab7a67606749e3a10722cbabd5092c__section_knq_5f3_vdb"/>

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

A File message pointing to the file or directory to be removed. The body is ignored. If it is a directory, *Remove All* must be set to true, otherwise an error is raised.

</td>
</tr>
</table>



<a name="loio34ab7a67606749e3a10722cbabd5092c__section_swc_cg3_vdb"/>

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

message.file

</td>
<td valign="top">

A message identical to the one received as input, indicating the operation happened successfully.

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

