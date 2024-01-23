<!-- loio43e1cc8d974b44fdaebd679d0984c920 -->

# Write File \(Deprecated\)

The Write File operator writes files to a storage service.



> ### Note:  
> This operator is deprecated.
> 
> Please use [Write File](write-file-7c3672c.md) instead.

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
> Use `Connection Management` for defining connections over the manual option.

The operation takes only one input parameter: the content of the file. The target file is configured in the operator's `path`. To dynamically change the target, see *Path formatting* below.



<a name="loio43e1cc8d974b44fdaebd679d0984c920__section_dwj_cq4_23b"/>

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

Mode

</td>
<td valign="top">

mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Controls whether the target file should be appended to, created \(avoiding overwrites, truncated if it already exists\), or overwritten \(created if it does not exist\). It may be dynamically set through the message header `storage.writeMode`.

Default: "append"

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

Holds information about connection information for the services. Only use manual connections when using a Connection ID is not possible.

Each service connection parameters is documented separately:

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

Configuration Type

</td>
<td valign="top">

configurationType

</td>
<td valign="top">

string

</td>
<td valign="top">

*connection parameter*

> ### Note:  
> It is recommended to choose : Which type of connection information will be used: Manual \(user input\) or retrieved by the Connection Management Service. *Configuration Manager* as the configuration type and select an existing *Connection ID*. The *Manual*: Which type of connection information will be configuration type must be used only for testing purposes.

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

A formatted string describing the output path for files. See Path formatting below for details and examples.

Default: "/tmp/file\\\_\\<counter\\\>.txt"

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

Terminate on Error

</td>
<td valign="top">

terminateOnError

</td>
<td valign="top">

boolean

</td>
<td valign="top">

A flag that indicates whether the graph should stop if this operator encounters an error. If set to False, an output may represent an error, in which case its attribute message.error will be True and its body will contain a string describing the error.

Default: "true"

</td>
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
</table>



<a name="loio43e1cc8d974b44fdaebd679d0984c920__section_gwj_cq4_23b"/>

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

`inFile` 

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose body \(blob\) will be written to a file. There are no requirements on the message's headers other than those referred to in the `path` and `mode` configuration parameters.

Default:

</td>
</tr>
</table>



<a name="loio43e1cc8d974b44fdaebd679d0984c920__section_iwj_cq4_23b"/>

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

`outFilename` 

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose body is the path to the file to which content is written or appended. Whether this path is relative or absolute depends on how it was given to the `path` configuration. The header`message.error` \(bool\) reports whether the operation was successful. Any other header from input is copied to this message.

</td>
</tr>
</table>



<a name="loio43e1cc8d974b44fdaebd679d0984c920__section_kwj_cq4_23b"/>

## Path Formatting

Strings in the `path` configuration are subject to the following rules:

-   Schemes can be invoked using angle brackets: The string `<foo>` will be replaced by the result of the scheme named "foo". Available schemes are:

    -   `counter`: an incremental integer

    -   `date`: the current local date in the format `YYYYMMDD`

    -   `time`: the current local time in the format `HHMMSS`


    Any other \(unrecognized\) scheme names will cause an error.

-   Message headers can be queried using `\${bar}`. For example, `\${bar}` would be replaced by the value of header "bar" in the message given to `inFile`. Note that the dollar sign must always be escaped with a backslash, otherwise it will be seen as a substitution parameter.
    -   A default value can be set using an equal sign: `\${bar=lorem}` will be replaced by the value "lorem" whenever the input message lacks the "bar" header. If no default value is set and the message is missing the header, an error will be thrown.

    -   It is necessary to escape the dollar sign with a backslash \(for example, `\${bar}`\) to prevent the Modeler from interpreting it as a substitution parameter.
    -   Anything else \(that is not between `<` and `>` or `\${` and `}`\) will be left untouched.




### Limitations

-   The following characters cannot appear in scheme or message header names: `<>${}`.

-   Empty scheme \(`<>`\) or header \(`\${}`\) names will be left untouched.




### Example: Basic Usage

Suppose you have messages coming from a Kafka Consumer whose topic describes the type of sensor that sent the message. Then you can use a path like this:

```
mydir_<date>_<time>/\${kafka.topic}.csv
```

It produces output files like this:

```
mydir_20170131_234550/noise.csv
mydir_20170201_080010/temperature.csv
mydir_20170201_080010/humidity.csv

```



### Example: Copying Directories

If we want to reproduce an entire directory structure, we can set a File, HDFS, or S3 Consumer to poll this directory and use the `storage.pathInPolledDirectory` header to refer to each file's location in it:

```
outputDir/\${storage.pathInPolledDirectory}
```

can be expanded to, for example:

```
outputDir/YearReport.docx
outputDir/January/sales.pdf
outputDir/January/finance.xlsx
outputDir/February/sales.pdf
```

