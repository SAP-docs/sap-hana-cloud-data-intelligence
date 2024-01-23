<!-- loiodf00dafec80f4b42afd2c9d22b395e30 -->

# Read File \(Deprecated\)

The Read File operator is used to read a file or periodically poll a directory for its contents in a storage service.



> ### Note:  
> This operator is deprecated.
> 
> Please use [Read File](read-file-bf64491.md) instead, possibly preceded by a [List Files](list-files-7060368.md) if dealing with directories.

> ### Note:  
> Limitation: The operator cannot browse at the root level of connections using a bucket or container, for example, S3, GCS, and WASB connections with root path / currently are not supported.

Supported services are:

-   [Local File System (/file)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/9cd7952d24f648d8babedda94a0a36af.html "Many of the SAP Data Intelligence storage operators offer support for the local file system.") :arrow_upper_right:
-   [Microsoft Azure Data Lake (ADL)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/e78850b420ec41728036e6bc01f4535f.html "Azure Data Lake (ADL) is Microsoft's Data Lake cloud storage service. Additional information, including the documentation, can be found at the official ADL Homepage.") :arrow_upper_right:
-   [Google Cloud Storage (GCS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/bd88d109721146a684cb47462864ccde.html "GCS is Google's Object Storage cloud service. Additional information, including the documentation, can be found at the official GCS Homepage.") :arrow_upper_right:
-   [Hadoop Distributed File System (HDFS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/d77575d3b41f41ef8eee5ade46ff7d84.html "Hadoop Distributed File System is Apache's distributed storage solution. For more information, see the official HDFS documentation.") :arrow_upper_right:
-   [Amazon Simple Storage Service (AWS S3)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/959ed43201ba4ef082016cb10e4ade6d.html "Many of the SAP Data Intelligence connectors support AWS S3, and there are common characteristics that this service has across the operators.") :arrow_upper_right:
-   [Microsoft Azure Blob Storage (WASB)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/5ecd01cac1524edba05aa4a262e3eeac.html "Azure Storage Blob (WASB) is one of Microsoft's cloud storage services. Additional information, including the documentation, can be found at the official WASB homepage.") :arrow_upper_right:
-   [WebHDFS](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/0978428f678e4ddaac88e59b18e9c915.html "WebHDFS supports Hadoop Distributed File System through the REST API. It is one of the protocols of Apache's distributed storage solution. For more information, see the official WebHDFS home page.") :arrow_upper_right:
-   [Alibaba Cloud Object Storage Service (OSS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/6b7c7eb2a990471fb604025327b9fd25.html "Many of the SAP Data Intelligence storage operators support the Alibaba Cloud OSS, and there are common characteristics that this service has across the operators.") :arrow_upper_right:

> ### Note:  
> Use Connection Management for defining connections over the manual option.

The operation takes only one input parameter: the path of the file. This is given as a string in the body of a message in the inPath port. If no input is connected to the port, the operator will periodically poll from the configured path.

The file content is output as the body of a message in the outFile port. Further details of the operation are reported as headers of the message, as listed in the port documentation.

An example of usage is given in the `com.sap.demo.file` graph.

Polling directories: When the given path points to a directory, this operator will poll all files inside that directory. It may be recursive if set to do so.

> ### Caution:  
> Reading large \(GB\) files in a single chunk may cause memory issues \(OOMKilled\). Use the `chunkSize` parameter in such cases.



<a name="loiodf00dafec80f4b42afd2c9d22b395e30__section_sq1_nf3_vdb"/>

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

Service

</td>
<td valign="top">

service

</td>
<td valign="top">

string

</td>
<td valign="top">

The file service to operate. Additional parameters may depend on the selected service.

Default: "file"

</td>
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

Holds information about the service's connections. Only use Manual connections when using a Connection ID is not possible.

Each service connection is documented separately:

-   [Microsoft Azure Data Lake (ADL)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/e78850b420ec41728036e6bc01f4535f.html "Azure Data Lake (ADL) is Microsoft's Data Lake cloud storage service. Additional information, including the documentation, can be found at the official ADL Homepage.") :arrow_upper_right:
-   [Google Cloud Storage (GCS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/bd88d109721146a684cb47462864ccde.html "GCS is Google's Object Storage cloud service. Additional information, including the documentation, can be found at the official GCS Homepage.") :arrow_upper_right:
-   [Hadoop Distributed File System (HDFS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/d77575d3b41f41ef8eee5ade46ff7d84.html "Hadoop Distributed File System is Apache's distributed storage solution. For more information, see the official HDFS documentation.") :arrow_upper_right:
-   [Amazon Simple Storage Service (AWS S3)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/959ed43201ba4ef082016cb10e4ade6d.html "Many of the SAP Data Intelligence connectors support AWS S3, and there are common characteristics that this service has across the operators.") :arrow_upper_right:
-   [Microsoft Azure Blob Storage (WASB)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/5ecd01cac1524edba05aa4a262e3eeac.html "Azure Storage Blob (WASB) is one of Microsoft's cloud storage services. Additional information, including the documentation, can be found at the official WASB homepage.") :arrow_upper_right:
-   [WebHDFS](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/0978428f678e4ddaac88e59b18e9c915.html "WebHDFS supports Hadoop Distributed File System through the REST API. It is one of the protocols of Apache's distributed storage solution. For more information, see the official WebHDFS home page.") :arrow_upper_right:
-   SDL
-   [Alibaba Cloud Object Storage Service (OSS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/6b7c7eb2a990471fb604025327b9fd25.html "Many of the SAP Data Intelligence storage operators support the Alibaba Cloud OSS, and there are common characteristics that this service has across the operators.") :arrow_upper_right:



</td>
</tr>
<tr>
<td valign="top">

Connection ID

</td>
<td valign="top">

connectionID

</td>
<td valign="top">

string

</td>
<td valign="top">

*connection parameter*: The ID of the connection information to retrieve from the Connection Management Service.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Connection Properties

</td>
<td valign="top">

connectionProperties

</td>
<td valign="top">

object

</td>
<td valign="top">

*connection parameter*: All the connection properties for the selected service for manual input.

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

A directory to be polled \(ends with `/`\) or a file to be read. This only applies if inPath is not connected.

Default: "/tmp/test.txt"

</td>
</tr>
<tr>
<td valign="top">

Delete After Send

</td>
<td valign="top">

deleteAfterSend

</td>
<td valign="top">

bool

</td>
<td valign="top">

A flag that indicates whether the file should be deleted after its contents have been sent.

> ### Caution:  
> There is no guarantee that the operator connected to the output receives the filename or content of the file.

> ### Note:  
> If `path` is a directory, the files in it will be removed after being read, but the directory itself will remain. When in recursive mode, subdirectories will also be kept.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Chunk Size

</td>
<td valign="top">

chunkSize

</td>
<td valign="top">

string

</td>
<td valign="top">

The maximum number of bytes that can be read from files at once. It reads the bytes in blocks until it reaches the end of the file. This can be used to reduce graph latency and memory usage.

If chunkSize is zero, files are read in a single chunk. Otherwise, it will be broken in chunks with a maximum size `chunkSize`. It may be dynamically customized through the message header `storage.chunkSize`. This field allows metric prefixes to be used and an optional "i" to indicate binary bases. For example:

-   `"0", "0B"`: unlimited

-   `"1", "1B"`: 1 byte

-   `"2kb", "2KB"`: 2\*103 bytes

    `"2kib", "2KiB"`: 2\*210 bytes

-   `"3mb", "3MB"`: 3\*106 bytes

-   `"3mib", "3MiB"`: 3\*220 bytes


Prefixes for Giga \(G\), Tera \(T\), and Peta \(P\) are also supported.

Default: "0"

</td>
</tr>
<tr>
<td valign="top">

Retry Attempts

</td>
<td valign="top">

numRetryAttempts

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of times to retry a connection.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Retry Period \(ms\)

</td>
<td valign="top">

retryPeriodInMs

</td>
<td valign="top">

int

</td>
<td valign="top">

The time interval in milliseconds between connection trials.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Poll Period \(ms\)

</td>
<td valign="top">

pollPeriodInMs

</td>
<td valign="top">

int

</td>
<td valign="top">

The time interval in milliseconds between successive polls. If no interval is needed, the value 0 should be used.

Default: 1000

</td>
</tr>
<tr>
<td valign="top">

Batch Read

</td>
<td valign="top">

batchRead

</td>
<td valign="top">

bool

</td>
<td valign="top">

A flag that controls whether all files should be read in batches. If set to True and a directory is a file, then it should be read in batches. If set to True and a directory is being polled, then outFilename is given a list with one filename per line polled, then outFilename is given a list with one filename per line \(may be empty when using `onlyReadOnChange`\); separated by CRLF \(may be empty when using `onlyReadOnChange`\).

Default: false

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

bool

</td>
<td valign="top">

A flag that controls whether a directory listing should recursively include all sub-directories.

Default: false

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

A regular expression used to filter file paths before reading them. If empty, all files are accepted. The expression is applied to a path after being converted to an absolute one only if one of the following is true:

-   It came from `inPath` and points to a regular file \(not a directory\).
-   It is a file found in the polled directory, regardless of whether the directory was specified by `inPath` or in `path`.

    For instance: the expression `^\/?(\w+\/)*[A-Za-z]\w+\.txt$` would match any path pointing to a file whose name starts with an alphabetic letter and ends with the extension `.txt`, such as `/foo/bar/file.txt` and `bar/f1.txt`, but not `file.csv` nor `/foo/bar/file`. The expression `(.txt)|(.csv)$` would match any file with `.txt` or `.csv` extension.


Default: ""

</td>
</tr>
<tr>
<td valign="top">

Only Read on Change

</td>
<td valign="top">

onlyReadOnChange

</td>
<td valign="top">

bool

</td>
<td valign="top">

If true, only outputs a file if it is new or changed, which avoids the repetitive reading of unchanged files.

This uses the date and time given by the file system as the latest modification time as opposed to the actual file contents. If using `batchRead`, a message with an empty body is outputted to `outFilename`, if no files were read, representing the empty list of files.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Terminate on Error

</td>
<td valign="top">

terminateOnError

</td>
<td valign="top">

boolean

</td>
<td valign="top">

A flag that indicates whether or not the graph should stop if this operator encounters an error. If set to `false`, an output may represent an error, in which case its attribute `message.error` will be `true` and its body will contain a string describing the error. This applies to whichever output port is connected.

Default: "true"

</td>
</tr>
<tr>
<td valign="top">

Configuration Type

</td>
<td valign="top">

configurationType

</td>
<td valign="top">

string

</td>
<td valign="top">

*connection parameter*: Which type of connection information will be used: Manual \(user input\) or retrieved by the Connection Management Service.

> ### Note:  
> It is recommended to choose *Configuration Manager* as the configuration type and select an existing *Connection ID*. The *Manual* configuration type must be used only for testing purposes.

Default: ""

</td>
</tr>
</table>



<a name="loiodf00dafec80f4b42afd2c9d22b395e30__section_knq_5f3_vdb"/>

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

inPath

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose body is the path \(relative or absolute\) of a file or directory \(ends with `/`\) to be read. When reading a single file, the message header `storage.offset` may be set to read a specific chunk from a file, which is also subject to the `chunkSize` configuration.

</td>
</tr>
</table>



<a name="loiodf00dafec80f4b42afd2c9d22b395e30__section_swc_cg3_vdb"/>

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

outFilename

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose body is the path of the file. This will be equal to the path that prompted the reading \(either `inPath` or <code><code>path</code></code>\).

</td>
</tr>
<tr>
<td valign="top">

outFile

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose headers describe the file read and whose body contains the file's contents as a blob. The message contains the following headers:

-   *storage.chunkIndex* \(type int\). The current chunk's index, starting from zero.
-   *storage.chunkCount* \(type int\). The total number of chunks for this file.
-   *storage.fileSize* \(type int64\). The size of the file, in bytes.
-   *storage.endOfFile* \(type bool\). A flag that indicates whether this chunk is the last \(this is simply a convenience: `endOfFile == (chunkIndex == chunkCount-1)`\).
-   *storage.filename* \(type string\). The name of the file, including extension \(if any\), but excluding its directory.
-   *storage.directory* \(type string\). The absolute path of the directory where the file resides.
-   *storage.path* \(type string\). The absolute path of the file \(equivalent to <`directory>/<filename>`\).
-   *storage.polledDirectory* \(type string\). The absolute path to the directory being polled, if applicable.
-   *storage.pathInPolledDirectory* \(type string\). The file path relative to`polledDirectory`. This is the result of subtracting `polledDirectory` from `directory`.
-   *storage.polledDirectorySize* \(type int64\). The total size of the directory, in bytes, if applicable.
-   *storage.fileIndex* \(type int64\). The index of the current file relative to a single request. Starts at `0` and is set to `0` if reading a single file.
-   *storage.fileCount* \(type int64\). The total number of files being read relative to a single request. Is set to `1` if reading a single file.
-   *storage.endOfSequence* \(type bool\). A flag that indicates if that is the last file of a given request \(this is simply a convenience: `endOfSequence == (fileIndex == fileCount-1)`\).
-   *message.error* \(type bool\). A flag that indicates whether the operation failed.



</td>
</tr>
</table>

