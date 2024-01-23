<!-- loioe04a4618fc514e14851437be651ab173 -->

# Monitor Files

This operator monitors file events in a directory from various storage services. Monitoring is achieved through listing files in the directory periodically.



Possible events are:

-   Already exists \(alreadyExists\): reported for any files already present in the directory when the graph starts;

-   New \(new\): a new file that was not present in the directory when the graph started, or a file that has been previously deleted and is recreated;

-   Modified \(modified\): the file has been modified compared to its previous state;

-   Deleted \(deleted\): the file previously found in the directory has been removed.


The reported file metadata is the last known one.

For each event, an output is generated as a file message with an additional `fileEvent` message attribute reporting the event. Each listing operation may also be tracked through the batching attributes.

The operator gets its connection according to the Connection property. You can use a static connection ID from Connection Management.

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



<a name="loioe04a4618fc514e14851437be651ab173__section_fct_pbw_zkb"/>

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

Points to the directory to be monitored, relative to the used connection. It must be in the qualified name format. If the Connection is set with a connection ID, you may use the UI file browsing to set the path.

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

Whether to monitor subdirectories recursively. If false, only the files at the first level of the requested path are monitored.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Events

</td>
<td valign="top">

events

</td>
<td valign="top">

object

</td>
<td valign="top">

Which events should be reported. Each property corresponds to an event that will be tracked if set to true. Each event is described in the beginning of this document.

Default: \{"alreadyExists":false,"new":true,"notModified":false,"modified":true,"deleted":false\}

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



## Input

None



<a name="loioe04a4618fc514e14851437be651ab173__section_fzk_q2w_zkb"/>

## Output

****


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

A file message with the an empty body. The message attribute `fileEvent` reports the event relative to the file. Possible events are described in the beginning of this document. The message also has the updated file metadata \(`connection`, `path`, `size`, `modTime` and `isDir`\) in the file attribute. It contains the batching attributes, except the `message.batchCount`, related to the list operation that occurs after every internal.

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

An error message, in case an error was raised during an operation.

</td>
</tr>
</table>

