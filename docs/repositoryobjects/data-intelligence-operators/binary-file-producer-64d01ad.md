<!-- loio64d01ad02e39499594b1eb103974443e -->

# Binary File Producer

The Binary File Producer operator writes files to various services.



A write operation happens at every input, either targeting a single file or a partitioned file depending on the configured `File Mode`.

Each operation uses a connection according to the configured `Connection`. And uses a path according to the configured `Path Mode`.

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
-   Local File System

    > ### Note:  
    > It does not use a Connection ID. It is the local file system of the environment in which the group containing this operator is running. Operators in a different group don't have access to it. Accessing any file or folder under the path `/vrep` is not supported and, while the operator may still run with such a configured path, it is unadvised.




<a name="loio64d01ad02e39499594b1eb103974443e__section_qdh_d3k_cjb"/>

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

Connection

</td>
<td valign="top">

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Points to the connection to write to. The connection configuration is detailed in File Messages. It uses the file connection attribute.

Default: \{"configurationType":"From input"\}

</td>
</tr>
<tr>
<td valign="top">

Path Mode

</td>
<td valign="top">

pathMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Indicates where the path is taken from.

Accepted values:

-   *Dynamic \(from input\)*: the path is taken from the `path` value of the input header `com.sap.headers.file`
-   *Static \(from configiration\)*: uses the `Path` configuration parameter.
-   *Static with placeholders*: uses the `Path` configuration parameter, allowing placeholders. More details at the [Path Placeholders](write-file-7c3672c.md#loio7c3672cb79874b21b41988ce7b5b690b__section_e4r_ljc_pkb) section found further below in this document.

Default: "Dynamic \(from input\)"

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

The path where the file is written to, relative to the connection being used. It must be in the qualified name format. If the `Connection` is set with a connection ID, you may use the UI file browsing to set the path. Only available if `Path Mode` is set to *Static \(from configuration\)* or *Static with placeholders*.

Default: /

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

Affects the behavior of the operation if the file already exists. If it does not exist, the operator always creates it.

Accepted values:

-   *Overwrite*: overwrites the existing file withh the content.

-   *Append*: appends the content to the end of the existing file.

-   *Create only*: does not change the file if it already exists. An error may or not be reported based on the `If File Exist Increment Name` configuration.


Default: Create only

</td>
</tr>
<tr>
<td valign="top">

If File Exist Increment Name

</td>
<td valign="top">

incrementName

</td>
<td valign="top">

bool

</td>
<td valign="top">

Only available if the `File Mode` is `Single File` and the Mode is `Create only`. If set to true, it will increment the file name suffix for an existing file.

Accepted values:

-   *False*: the `errorHandling` will decide what happens if the file exists.

-   *True*: the file name receives a number suffix that doesn't exist yet. For example, if path is configured to `file.txt` and it already exists, the file name becomes `file (1).txt`. If `file (1).txt` also exists, then `file (2).txt` is used and so on.

Default: false

</td>
</tr>
<tr>
<td valign="top">

File Mode

</td>
<td valign="top">

fileMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Indicates whether the target file is a single file or a partitioned file. More details on the behavior of both options on the [File Modes](binary-file-producer-64d01ad.md#loio64d01ad02e39499594b1eb103974443e__section_t35_1yt_qqb) section available further below in this document.

Accepte values:

-   *Single file*: writes input to a simple, single file.

-   *Partitioned file*: writes input to a partitioned file, using batch information to determine which file to write to.


Default: Single file

</td>
</tr>
<tr>
<td valign="top">

Error Handling

</td>
<td valign="top">

errorHandling

</td>
<td valign="top">

string

</td>
<td valign="top">

Details available at [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:.

Default: "terminate on error"

</td>
</tr>
</table>



<a name="loio64d01ad02e39499594b1eb103974443e__section_knq_5f3_vdb"/>

## Input


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Kind

</th>
<th valign="top">

Type ID

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

scalar

</td>
<td valign="top">

com.sap.core.binary

</td>
<td valign="top">

A binary input whose body is used as the content to be written. The `connection` and `path` values from the `com.sap.headers.file` header may be used as well, according to the operator configuration.

</td>
</tr>
</table>



<a name="loio64d01ad02e39499594b1eb103974443e__section_swc_cg3_vdb"/>

## Output


<table>
<tr>
<th valign="top">

Output

</th>
<th valign="top">

Kind

</th>
<th valign="top">

Type ID

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

none

</td>
<td valign="top">

""

</td>
<td valign="top">

An output with an empty body and the `com.sap.headers.file` header set with the metadata of the file written, particularly the fields `connection` and `path`. The output is sent only when the file is completely written, be it after the input for writing a single file or on the last input when writing a partitioned file.

</td>
</tr>
<tr>
<td valign="top">

error

</td>
<td valign="top">

structure

</td>
<td valign="top">

com.sap.error

</td>
<td valign="top">

An error message as described at [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:.

</td>
</tr>
</table>



<a name="loio64d01ad02e39499594b1eb103974443e__section_e4r_ljc_pkb"/>

## Path Placeholders

Path placeholders allow dynamic values as part of the path. They can be invoked using angle brackets: the string `<counter>` is replaced by the result of the placeholder named `counter`.

Some placeholders also have a suffix, defined after the colon separator \(`:`\).

> ### Example:  
> The string `<header:headerName>` points to the placeholder `header` with the suffix `headerName`.

Available placeholders are:


<table>
<tr>
<th valign="top">

Placeholder

</th>
<th valign="top">

Description

</th>
<th valign="top">

Original Path Example

</th>
<th valign="top">

Generated Path Example

</th>
</tr>
<tr>
<td valign="top">

counter

</td>
<td valign="top">

An incremented integer.

</td>
<td valign="top">

Take the following path:

-   `/folder/file_<counter>.txt`



</td>
<td valign="top">

It generates sequential operations on the paths:

-   `/folder/file_000001.txt`
-   `/folder/file_000002.txt`
-   `/folder/file_000003.txt`



</td>
</tr>
<tr>
<td valign="top">

date

</td>
<td valign="top">

The current local date in the format `YYYYMMDD`.

</td>
<td valign="top">

Take the following path:

-   `/folder/file_<date>.txt`



</td>
<td valign="top">

It considers the server's current date \(such as 01/16/2020 - January 16th 2020\) and daily writing operations to generate the following paths:

-   `/folder/file_20201216.txt`
-   `/folder/file_20201217.txt`
-   `/folder/file_20201218.txt`

If more than one operation is performed on the same day, the date remains the same:

-   `/folder/file_20201216.txt`
-   `/folder/file_20201216.txt`
-   `/folder/file_20201216.txt`



</td>
</tr>
<tr>
<td valign="top">

time

</td>
<td valign="top">

The current local time in the format `HHMMSS`.

</td>
<td valign="top">

Take the following path:

-   `/folder/file_<time>.txt`



</td>
<td valign="top">

It considers the server's current time \(such as 22h 27min 33s\) and a writing operation performed at each second to generate the following paths:

-   `/folder/file_102733.txt`
-   `/folder/file_102734.txt`
-   `/folder/file_102735.txt`

If more than one operation occurs at the same second, the time remains the same:

-   `/folder/file_102733.txt`
-   `/folder/file_102733.txt`



</td>
</tr>
<tr>
<td valign="top">

dirname

</td>
<td valign="top">

The directory prefix extracted from the incoming path. Requires an input path attribute \(`file.path`\).

</td>
<td valign="top">

Take the following path:

-   `<dirname>/file.txt`




</td>
<td valign="top">

Consider that the input port message has the `file` key attribute with the value object `{ "path": "/myfolder/mysubfolder/myfile.txt" }`, it generates:

-   `/myfolder/mysubfolder/file.txt`


If the prefix includes a leading slash, that is also taken as part of the placeholder. Taking the previous input, a configured path like`/rootdir<dirname>/file.txt` would result in `/rootdir/myfolder/mysubfolder/file.txt`.

</td>
</tr>
<tr>
<td valign="top">

basename

</td>
<td valign="top">

The base file name extracted from the incoming path. Requires an input path attribute \(`file.path`\).

</td>
<td valign="top">

Take the following path:

-   `/folder/<basename>`




</td>
<td valign="top">

Consider that the input port message has the `file` key attribute with the value object `{ "path": "/mydir/mysubdir/myfile.txt" }`, it generates:

-   `/folder/myfile.txt`




</td>
</tr>
<tr>
<td valign="top">

extension

</td>
<td valign="top">

The extension extracted from the incoming path without the leading dot \(`.`\). Requires an input path attribute \(`file.path`\).

</td>
<td valign="top">

Take the following path:

-   `/folder/file.<extension>`




</td>
<td valign="top">

Consider that the input port message has the `file` key attribute with the value object `{ "path": "/mydir/mysubdir/myfile.txt" }`, it generates:

-   `/folder/fil.txt`




</td>
</tr>
<tr>
<td valign="top">

multiplicity

</td>
<td valign="top">

The multiplicity of the operator's group.

</td>
<td valign="top">

Take the following path:

-   `/folder/file_<multiplicity>.txt`



</td>
<td valign="top">

It uses the multiplicity total according to where the operator is located. Default is 1 when the operator is not grouped.

If the operator is grouped and *Multiplicity* is set to `3`, it generates:

-   `/folder/file_3.txt`



</td>
</tr>
<tr>
<td valign="top">

multiplicityIndex

</td>
<td valign="top">

An integer in the range `[0,multiplicity)` that can be used to distinguish the multiple instances of this operator.

</td>
<td valign="top">

Take the following path:

-   `/folder/file_<multiplicityIndex>.txt`



</td>
<td valign="top">

If the operator is grouped and *Multiplicity* is set to `3`, three instances of the Binary File Producer operator are generated, each with a different `index` \(`0`, `1` and `2`\).

It can generate one of the following paths, depending on which Binary File Producer performed the operation:

-   `/folder/file_0.txt`
-   `/folder/file_1.txt`
-   `/folder/file_2.txt`



</td>
</tr>
<tr>
<td valign="top">

header

</td>
<td valign="top">

Queries the input message for a specified attribute. Requires a suffix with the message attribute key to be queried. For example, `<header:my_header>`.

</td>
<td valign="top">

Take the following path:

-   `/folder/file.<header:fileFormat>`



</td>
<td valign="top">

Considering that the input port message has a `fileFormat` key attribute with the `csv` value, it generates:

-   `/folder/file.csv`

If key attribute is `fileFormat` and its value `txt`, it generates:

-   `/folder/file.txt`



</td>
</tr>
</table>



<a name="loio64d01ad02e39499594b1eb103974443e__section_t35_1yt_qqb"/>

## File Modes

The behavior for the *Single file* mode is to write to the target path at each input, outputting the target file metadata on success.

Each input writes to the configured path. If `Path Mode` is *From input*, the path is always taken from the current input. If `Path Mode` is *Static with placeholders*, **Path Placeholders** are reevaluated at each input.

If on *Partitioned file* mode, a folder is created on the configured path, following the same rules from the *Single file* mode. Part files are written inside this folder, including an eventual indicator file at the end of the operation.

In this mode, the input messages must have the **batch header** information set, with the required**batch index** and **is last** fields. The index is used to write to different part files on the file system.

Each batch implies a different part file being written. All parts imply a single complete file write operation. Therefore, all the checks and path processing necessary for the operation happen once at the beginning of the complete file write operation. The beginning here is defined as the arrival of a message with the **batch index equal to 0**.

Each operator `Mode` has a different behavior when the `File Mode` is set to *Partitioned file*, as follows:

-   *Overwrite* recursively removes a file or a directory and its contents on the target path, then starts writing the first batch.

-   *Append* checks for the presence of a valid partitioned file on the path. A partitioned append can't be executed on a single file. If the check is successful, the indicator `_SUCCESS` file is removed, and the operation starts. Notably, the appended data starts on the `index` 0, with a different `uuid`.
-   *Create Only* checks the destination path for the presence of a file or folder. If it is present, the operation fails; otherwise, it starts.



<a name="loio64d01ad02e39499594b1eb103974443e__section_pkf_3zt_qqb"/>

## State Management Support

When writing with `File Mode` set to *Single file*, no state management support is possible, as we don't support partial writes to the target file.

State management support is provided when `File Mode` is set to *Partitioned file*, with **Exactly once** guarantee. The state is saved between part file writes, so upon recovery, the graph doesn't have to start writing from the first file. Instead, writing starts from the first received index once the graph is resumed.

If the `Connection` is set to *Local File System*, no state management support is possible since a local file system no longer exists once the graph reaches the Completed, Dead, or Paused status.

