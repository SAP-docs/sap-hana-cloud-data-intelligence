<!-- loio9a9319af144944c481705698ad8985e6 -->

# Copy File \(Deprecated\)

The Copy File operator is used to copy files in a storage service. The expected input message is specified in the Input section in this topic.



> ### Note:  
> This operator is deprecated. Use the operators [Read File](read-file-bf64491.md) and [Write File](write-file-7c3672c.md) to perform the same action.
> 
> Additionaly, [List Files](list-files-7060368.md) can be used to move directories.

This operation is recursive, meaning it will copy any file or directory under the given source path.

If destination is a file, it will be overwritten; if it is a non-empty directory, it will fail.

Supported services are:

-   [Google Cloud Storage (GCS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/bd88d109721146a684cb47462864ccde.html "GCS is Google's Object Storage cloud service. Additional information, including the documentation, can be found at the official GCS Homepage.") :arrow_upper_right:

-   [Amazon Simple Storage Service (AWS S3)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/959ed43201ba4ef082016cb10e4ade6d.html "Many of the SAP Data Intelligence connectors support AWS S3, and there are common characteristics that this service has across the operators.") :arrow_upper_right:

-   [Microsoft Azure Blob Storage (WASB)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/5ecd01cac1524edba05aa4a262e3eeac.html "Azure Storage Blob (WASB) is one of Microsoft's cloud storage services. Additional information, including the documentation, can be found at the official WASB homepage.") :arrow_upper_right:

-   [Alibaba Cloud Object Storage Service (OSS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/6b7c7eb2a990471fb604025327b9fd25.html "Many of the SAP Data Intelligence storage operators support the Alibaba Cloud OSS, and there are common characteristics that this service has across the operators.") :arrow_upper_right:

Use `Connection Management` for defining connections over the manual option.

> ### Note:  
> This operator supports only services that have such operations available. On other services, *Copy* can be achieved through *Read* + *Write*.
> 
> **Behavior Example**
> 
> In the given file structure:
> 
> ```
> .
> .
> |
> +-- a
> |   +-- file1.txt
> |   +-- file2.txt
> +-- b
>     +-- f1.txt
>     +-- f2.txt
> ```

-   Copying source `a/file1.txt` to destination `newfile.txt` would succeed because the destination does not exist.

-   Copying source `a/file1.txt` to destination `b/f1.txt` would succeed and overwrite `b/f1.txt` because the destination is an existing file.

-   Copying source `a/file1.txt` to destination: `b/` would fail because `b/` already exists and is not empty.

-   Copying source `a/` to destination `b/` would fail because `b/` already exists and is not empty.

-   Copying source `a/` to destination `b/dir/` would succeed because `b/dir/` does not exist.




<a name="loio9a9319af144944c481705698ad8985e6__section_sq1_nf3_vdb"/>

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

Default: "GCS"

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

Holds information about the service's connections. Only use manual connections when using a connection ID is not possible.

Each service connection parameters is documented separately:

-   [Google Cloud Storage (GCS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/bd88d109721146a684cb47462864ccde.html "GCS is Google's Object Storage cloud service. Additional information, including the documentation, can be found at the official GCS Homepage.") :arrow_upper_right:
-   [Amazon Simple Storage Service (AWS S3)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/959ed43201ba4ef082016cb10e4ade6d.html "Many of the SAP Data Intelligence connectors support AWS S3, and there are common characteristics that this service has across the operators.") :arrow_upper_right:
-   [Microsoft Azure Blob Storage (WASB)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/5ecd01cac1524edba05aa4a262e3eeac.html "Azure Storage Blob (WASB) is one of Microsoft's cloud storage services. Additional information, including the documentation, can be found at the official WASB homepage.") :arrow_upper_right:
-   [Alibaba Cloud Object Storage Service (OSS)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/6b7c7eb2a990471fb604025327b9fd25.html "Many of the SAP Data Intelligence storage operators support the Alibaba Cloud OSS, and there are common characteristics that this service has across the operators.") :arrow_upper_right:



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

*connection parameter* Which type of connection information will be used: Manual \(user input\), or retrieved by the Connection Management Service.

> ### Note:  
> It is recommended to choose *Configuration Manager* as the configuration type and select an existing *Connection ID*. The *Manual* configuration type must be used only for testing purposes.

Default: ""

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

*connection parameter* The ID of the connection information to retrieve from the Connection Management Service.

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

*connection parameter* All the connection properties for manual input.

</td>
</tr>
<tr>
<td valign="top">

Timeout \(ms\)

</td>
<td valign="top">

timeoutInMs

</td>
<td valign="top">

int

</td>
<td valign="top">

Sets the time limit to execute the operation. If 0, no timeout is used.

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

Simultaneous Requests

</td>
<td valign="top">

simultaneousRequests

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of simultaneous requests generated on recursive calls \(only available for GCS, S3, and WASB\).

Default: 1

</td>
</tr>
<tr>
<td valign="top">

Stop Requests on Error

</td>
<td valign="top">

stopRequestOnError

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Controls whether simultaneous requests from recursive calls should stop at first error \(only available for GCS, S3, and WASB\).

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

A flag that indicates whether the graph should stop if this operator encounters an error. If set to `false`, an output may represent an error, in which case its attribute `message.error` will be `true` and its body will contain a string describing the error.

Default: true

</td>
</tr>
</table>



<a name="loio9a9319af144944c481705698ad8985e6__section_knq_5f3_vdb"/>

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

`in` 

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose body has the source file path and destination. Expected message attributes:

*storage.src* Mandatory. Path to source file or directory.

*storage.dst* Mandatory. Path to destination file or directory \(should match types with source\). The destination path may contain `<dirname>` and `<basename>`, referring to the given source path's dirname and basename. For example, `move src:data/A/user.csv dst:<dirname>/processedFiles/<basename>` would map to the destination `data/A/processedFiles/user.csv`.

*storage.srcBucket* Overrides `bucket` from configuration on service GCS and S3 for the source file or directory.

*storage.dstBucket* Overrides `bucket` from configuration on service GCS and S3 for the destination file or directory.

</td>
</tr>
</table>



<a name="loio9a9319af144944c481705698ad8985e6__section_swc_cg3_vdb"/>

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

`out` 

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose header `message.error` \(bool\) reports whether the operation was successful. The body and any other header from the input message are copied to this one.

</td>
</tr>
</table>

