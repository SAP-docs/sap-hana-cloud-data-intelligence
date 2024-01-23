<!-- loio1faddfa3f3e14bcb98049e90ece74f1f -->

# Binary File Consumer

The Binary File Consumer operator reads the content of files from various storage services.



A read operation happens according to the *Read* configuration. If reading `On input`, the input contains the used path. Otherwise, if reading `Once`, the path comes from the configuration.

The connection used varies with the *Connection* configuration. The *Connection type* `From input` is available only if reading `On input`. Otherwise, a static connection ID from `Connection Management` connection can be used.

Supported services are:

-   Alibaba Cloud Object Storage Service \(OSS\).

-   Amazon Simple Storage Service \(S3\).
-   Google Cloud Storage \(GCS\).
-   Hadoop Distributed File System \(HDFS\).
-   HANA Data Lake \(HDL\_FILES\)
-   Microsoft Azure Data Lake \(ADL\).
-   Microsoft Azure Data Lake Gen. 2 \(ADL\_V2\).
-   Microsoft Windows Azure Storage Blobs \(WASB\).
-   Semantic Data Lake \(SDL\).
-   SSH File Transfer Protocol \(SFTP\).
-   Local File System.

    > ### Note:  
    > It does not use a Connection ID. It is the local file system of the environment in which the group containing this operator is running. Operators in a different group don't have access to it. Accessing any file or folder under the path `/vrep` is not supported and, while the operator may still run with such a configured path, it is unadvised.




<a name="loio1faddfa3f3e14bcb98049e90ece74f1f__section_yjs_x2l_ntb"/>

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

Mandatory. Sets the operation mode. Find details of each mode below.

-   `On input`: a read operation happens for every input received. The input informs the path to read from.

-   `Once`: a single read operation happens as soon as the graph is ***Running***. The *Path* configuration informs the path to read from.

Default: `"On input"`

</td>
</tr>
<tr>
<td valign="top">

Connection \(static\)

</td>
<td valign="top">

staticConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Points to the static connection to read from. Only available if *Read* is set to `Once`.

Default: `{}`

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

Points to the dynamic connection to read from. It uses the `connection` field from each record from the `com.sap.file.info.table`. Only available if *Read* is set to `On input`.

Default: `{"configurationType":"From input"}`

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

It can either point to the file to be read, or a valid directory containing a partitioned file, relative to the used connection. It must be in the qualified name format. If the *Connection* is set with a connection ID, you may use the UI file browsing to set the path. Only available if *Read* is set to `Once`.

Default: `/`

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

Default: `"terminate on error"`

</td>
</tr>
</table>



<a name="loio1faddfa3f3e14bcb98049e90ece74f1f__section_fjp_mgl_ntb"/>

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

none

</td>
<td valign="top">

""

</td>
<td valign="top">

An input with an empty body containing the `com.sap.headers.file`, which can point to a single file or a valid directory containing a partitioned file.

> ### Note:  
> In both cases it is expected that the `isDir` property of the `com.sap.headers.file` header is set to `false`.

This is only applicable when *Read* mode is set to `On Input`.

</td>
</tr>
</table>



<a name="loio1faddfa3f3e14bcb98049e90ece74f1f__section_tm5_qgl_ntb"/>

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

scalar

</td>
<td valign="top">

com.sap.core.binary

</td>
<td valign="top">

A blob with the contents of a file. The header `com.sap.headers.file` contains the file information related to the output.

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

An error message as described at [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:. It depends on the *Error Handling* configuration.

</td>
</tr>
</table>



<a name="loio1faddfa3f3e14bcb98049e90ece74f1f__section_dcx_c5l_3vb"/>

## Snapshot Support

Snapshot support is provided when *Read* is set to `Once` and the target path is a directory containing a partitioned file, with `at-least-once` guarantee.

The state is saved between parts, so upon recovery, the operator doesn't have to start reading them from the start.

Instead, the read starts from the last part index saved once the graph is resumed.

