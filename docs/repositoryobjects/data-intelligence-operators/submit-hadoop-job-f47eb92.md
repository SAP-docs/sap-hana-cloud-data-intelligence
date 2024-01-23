<!-- loiof47eb929060d4534a0ca8a022fad1eea -->

# Submit Hadoop Job

The Submit Hadoop Job operator is used to submit jobs to Hadoop clusters provided by different cloud providers. Currently the only supported Hadoop cluster type is Google Dataproc.



Supported services:

-   Google Dataproc \(Spark, PySpark, SparkSQL, Hive\)

The operator has one input port: `jobConfig`, which is optional and used to dynamically overwrite static configurations. A dynamic job configuration is represented as a JSON object, whose structure depends on a job type and a service provider. See examples of job configurations below.

The operator has one output port: `result`. The output is represented as a message with attributes containing metadata. For example, each message will have a cluster and job configuration in its attributes as well as specific attributes for each job type. The message contains a key named `message.error`, which is `true` in case of failure and `false` in case of success.

A dynamic Dataproc Spark job configuration can look like the example below \(include only needed fields\):

```
{
  "sparkJobSpec": {
    "mainJarFileUri":"gs://bucket/file.jar",
    "mainClass": "org.apache.spark.ClassName",
    "args": ["10"],
    "fileUris": ["gs://bucket/file1.txt","gs://bucket/file2.txt"],
    "jarFileUris": ["gs://bucket/jar1.jar", "gs://bucket/jar2.jar"],
    "archiveUris": ["models1.zip", "models2.zip"],
    "properties": {"prop1": "v1", "prop2": "v2"},
    "dataprocSparkDriverLogLevels": {"org.apache.spark": "DEBUG"}
  },
  "labels": {"label1": "v1", "label2": "v2"}
}
```

Next, an examaple for dynamic Dataproc Spark SQL job configuration \(include only needed fields\):

```
{
  "sparkSqlJobSpec": {
    "queryList": {"queries": ["DROP TABLE t2"]},
    "scriptVariables": {"a": "b", "spark.property": "20"},
    "fileUris": ["gs://bucket/file1.txt","gs://bucket/file2.txt"],
    "jarFileUris": ["gs://bucket/jar1.jar"],
    "properties": {"prop1": "v1", "prop2": "v2"},
    "dataprocSparkDriverLogLevels": {"org": "DEBUG"}
  },
  "labels": {"label1": "v1", "label2": "v2"}
}
```

A dynamic Dataproc PySpark job configuration can look like \(include only needed fields\):

```
{
  "pySparkJobSpec": {
    "mainPythonFileUri":"gs://bucket/file.py",
    "args": ["10"],
    "pythonFileUris": ["gs://bucket/f1.py","gs://bucket/f2.py"],
    "fileUris": ["gs://bucket/file1.txt","gs://bucket/file2.txt"],
    "jarFileUris": ["gs://bucket/jar1.jar", "gs://bucket/jar2.jar"],
    "archiveUris": ["models1.zip", "models2.zip"],
    "properties": {"prop1": "v1", "prop2": "v2"},
    "dataprocSparkDriverLogLevels": {"org.apache.spark": "DEBUG"}
  },
  "labels": {"label1": "v1", "label2": "v2"}
}
```

Finally, a Dataproc Hive job configuration example \(include only needed fields\):

```
{
  "hiveJobSpec": {
    "queryList": {"queries": ["DROP TABLE t2"]},
    "scriptVariables": {"a": "b", "hive.property": "20"},
    "fileUris": ["gs://bucket/file1.txt","gs://bucket/file2.txt"],
    "jarFileUris": ["gs://bucket/jar1.jar"],
    "properties": {"prop1": "v1", "prop2": "v2"},
    "dataprocSparkDriverLogLevels": {"org": "DEBUG"}
  },
  "labels": {"label1": "v1", "label2": "v2"}
}
```

See the `com.sap.demo.hadoop.dataproc` example graph to check how to use this operator.



<a name="loiof47eb929060d4534a0ca8a022fad1eea__section_pmq_bh3_cfb"/>

## Configuration Parameters

**Universal Configurations**


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

Job Type

</td>
<td valign="top">

dataprocJobType

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory: A Dataproc job type.

Default: "spark"

</td>
</tr>
<tr>
<td valign="top">

Labels

</td>
<td valign="top">

dataprocLabels

</td>
<td valign="top">

string

</td>
<td valign="top">

Labels to associate with the Dataproc job.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Driver Log Levels

</td>
<td valign="top">

dataprcoSparkDriverLogLevels

</td>
<td valign="top">

string

</td>
<td valign="top">

Spark driver log levels represented as a JSON object.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Jar File URIs

</td>
<td valign="top">

dataprocJarFileUris

</td>
<td valign="top">

string

</td>
<td valign="top">

Jar file URIs separated by ','.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Spark Command Arguments

</td>
<td valign="top">

dataprocSparkArgs

</td>
<td valign="top">

string

</td>
<td valign="top">

Spark job arguments separated by ','.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Spark Configuration

</td>
<td valign="top">

dataprocSparkConf

</td>
<td valign="top">

string

</td>
<td valign="top">

Spark configurations. Similar to --conf parameters of spark-submit but as a JSON object.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

File URIs

</td>
<td valign="top">

dataprocSparkFileUris

</td>
<td valign="top">

string

</td>
<td valign="top">

Spark file URIs separated by ','..

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Archive URIs

</td>
<td valign="top">

dataprocSparkArchiveUris

</td>
<td valign="top">

string

</td>
<td valign="top">

Spark aarchive URIs separated by ','.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Connection

</td>
<td valign="top">

dataprocConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

GCP Dataproc connection details used to connect to the service.

Default: ""

</td>
</tr>
</table>

**Connection Parameters**


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

Configuration Type

</td>
<td valign="top">

configurationType

</td>
<td valign="top">

string

</td>
<td valign="top">

The type of connection information is used: Manual \(user input\) or retrieved by the Connection Management Service.

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

The ID of the connection information to retrieve from the Connection Management Service.

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

All the connection properties for manual input.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Project ID

</td>
<td valign="top">

projectId

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The GCP Project ID.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Cluster Name

</td>
<td valign="top">

clustesName

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Name of the cluster the job is sent to.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Region

</td>
<td valign="top">

region

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The region in which the cluster is located.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Zone

</td>
<td valign="top">

zone

</td>
<td valign="top">

string

</td>
<td valign="top">

The zone in which the cluster is located.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Keyfile

</td>
<td valign="top">

keyfile

</td>
<td valign="top">

string

</td>
<td valign="top">

JSON key file used to authenticate and access secured clusters.

Default: ""

</td>
</tr>
</table>

**Spark Configurations**


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

Main Jar File URI

</td>
<td valign="top">

dataprocSparkMainJarFileUri

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The main Sparj jar file URI.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Class Name

</td>
<td valign="top">

dataprocSparkClassName

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. A class name to execute.

Default: ""

</td>
</tr>
</table>

**PySpark Configurations**


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

Main Python File URI

</td>
<td valign="top">

dataprocSparkMainPythonFileUri

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The main PySpark file URI.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Python File URIs

</td>
<td valign="top">

dataprocSparkPythonFileUris

</td>
<td valign="top">

string

</td>
<td valign="top">

Additional Python file URIs separated by ','.

Default: ""

</td>
</tr>
</table>

**Hive Configurations**


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

Continue on failure

</td>
<td valign="top">

dataprocHiveContinueOnFailure

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. A flag that determines whether to continue executing Hive queries if a query fails.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Hive Configuration

</td>
<td valign="top">

dataprocHiveConf

</td>
<td valign="top">

string

</td>
<td valign="top">

Hive configurations represented as a JSON object.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Query File URI

</td>
<td valign="top">

dataprocHiveQueryFileUri

</td>
<td valign="top">

string

</td>
<td valign="top">

A file URI with Hive queries.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Queries

</td>
<td valign="top">

dataprocHiveQueries

</td>
<td valign="top">

string

</td>
<td valign="top">

A text field for Hive queries.

> ### Note:  
> It cannot be used in conjunction with Query Files.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Script Variables

</td>
<td valign="top">

dataprocHiveScriptVariables

</td>
<td valign="top">

string

</td>
<td valign="top">

A field for Hive script variables. Equivalent to the Hive command: SET name="value".

Default: ""

</td>
</tr>
</table>

**SparkSQL Configurations**


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

Query File URI

</td>
<td valign="top">

dataprocSparkSqlQueryFileUri

</td>
<td valign="top">

string

</td>
<td valign="top">

A file URI with Spark SQL queries.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Queries

</td>
<td valign="top">

dataprocSparkSqlQueries

</td>
<td valign="top">

string

</td>
<td valign="top">

A text field for Spark SQL queries.

> ### Note:  
> It cannot be used in conjunction with Query Files.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Script Variables

</td>
<td valign="top">

dataprocSparkSqlScriptVariables

</td>
<td valign="top">

string

</td>
<td valign="top">

A field for Spark SQL variables. Equivalent to the Spark SQL command: SET name="value".

Default: ""

</td>
</tr>
</table>

> ### Note:  
> All Python and Jar files referenced must be from a HDFS or HDFS-compatible file system, or located in a Google Cloud Storage bucket. For more information, you can refer to the Dataproc v1 API documentation at [https://developers.google.com/resources/api-libraries/documentation/dataproc/v1/csharp/latest/namespaceGoogle\_1\_1Apis\_1\_1Dataproc\_1\_1v1\_1\_1Data.html](https://developers.google.com/resources/api-libraries/documentation/dataproc/v1/csharp/latest/namespaceGoogle_1_1Apis_1_1Dataproc_1_1v1_1_1Data.html)



<a name="loiof47eb929060d4534a0ca8a022fad1eea__section_knq_5f3_vdb"/>

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

`jobConfig` 

</td>
<td valign="top">

string

</td>
<td valign="top">

A JSON object representing a dynamic job configuration, which overwrites or appends the static properties.

</td>
</tr>
</table>



<a name="loiof47eb929060d4534a0ca8a022fad1eea__section_swc_cg3_vdb"/>

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

`result` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The operator sends a message with the used jobs' attributes and a flag whether the job was successful when finished.

</td>
</tr>
</table>

