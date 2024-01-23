<!-- loiocaf0066d15454d379ef71ad1a157f5bc -->

# Livy Spark Submit

This operator submits jobs to a cluster using the Livy REST API. It has 2 different modes: jar and snippet.



When one mode is chosen, the configuration tab will show only relevant configuration parameters.

1.  In jar mode, you can submit an application in a way that is very similar to using spark-submit. The operator will succeed only if the underlying job is finished successfully. For instance, if a jar file is submitted to YARN, the operator status will be identical to the application status in YARN. Note that the jar file must be accessible to Livy.

2.  In snippet mode, code snippets could be sent to a Livy session and results will be returned to the output port. This approach is very similar to using the Spark shell. Please, note that there are some limitations in adding jars to sessions due to LIVY-327.

    As opposed to jar mode, the operator will not fail even if a code snippet sent to Livy is failed. You can change this default behavior by setting strictCodeExecutionMode to true in the configuration tab.

    -   In strict mode, the operator verifies if the output of the code snippet execution contains any errors. If any errors are found, the operator will also fail.

    -   In non-strict mode, the operator will ignore possible errors that happen during the snippet execution. As a consequence, users have to analyze the result manually to see if the execution is successful. This can be done by exploring the job execution output, which is sent to the output port of the operator.





<a name="loiocaf0066d15454d379ef71ad1a157f5bc__section_sq1_nf3_vdb"/>

## Configuration Parameters

Users are responsible for setting mandatory configuration parameters. If default values are not changed, they will be sent to the target Livy endpoint, which can lead to errors. On the contrary, if \(ptional \)configuration parameters are not changed, they will not be included in requests to Livy.

Common configurations:


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

Livy Endpoint

</td>
<td valign="top">

livyEndopoint

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Defines the Livy endpoint to use \(please, also specify the port number\). If the Livy service cannot be reached - the operator will fail during the initialization phase.

Default: "http://livy-api-endpoint.com:8998"

</td>
</tr>
<tr>
<td valign="top">

Validate Host Certificate

</td>
<td valign="top">

validateCertificate

</td>
<td valign="top">

bool

</td>
<td valign="top">

A flag indicating whether the server certificate will be validated when connecting with TLS.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Source Type

</td>
<td valign="top">

sourceType

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Defines the type of the job that is being submitted: "jar" for using a jar-file, "snippet" - for a snippet of code.

Default: "jar"

</td>
</tr>
<tr>
<td valign="top">

Error Handling Mode

</td>
<td valign="top">

errorHandlingMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Defines the error handling mode:

-   in "default" mode, any errors from the Livy operator are immediately returned to the execution engine. As a consequence, the whole graph is failed and the remaining part of your pipeline is not executed.

-   in "pipeline" mode, all errors are streamed to the error port and the execution continues. This mode allows you to have different pipelines depending on the status of your Spark job submitted by Livy.

Default: "default"

</td>
</tr>
<tr>
<td valign="top">

Proxy User

</td>
<td valign="top">

proxyUser

</td>
<td valign="top">

string

</td>
<td valign="top">

User to impersonate when starting a session or running a job. It's also used as a value of the "X-Requested-By" header in HTTP requests to avoid being blocked by the CSRF protection. If this value is empty, "X-Requested-By" will be equal to "hdfs".

Default: "hdfs"

</td>
</tr>
<tr>
<td valign="top">

Jars

</td>
<td valign="top">

jars

</td>
<td valign="top">

string

</td>
<td valign="top">

Jars to be used in this session or batch.

Default: "jar1,jar2,..."

</td>
</tr>
<tr>
<td valign="top">

Configuration

</td>
<td valign="top">

conf

</td>
<td valign="top">

string

</td>
<td valign="top">

The value for the "--conf" argument of spark-submit. You must input configurations exactly according to the JSON-format, and **wrap it with curly braces**.

Default: "\{"key1":"value1","key2":"value2"\}"

</td>
</tr>
<tr>
<td valign="top">

Access Token

\(For jar mode only\)

</td>
<td valign="top">

accessToken

</td>
<td valign="top">

string

</td>
<td valign="top">

OAuth access token.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Batch Name

\(For jar mode only\)

</td>
<td valign="top">

batchName

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the batch.

Default: "default batch name"

</td>
</tr>
<tr>
<td valign="top">

Jar Path

\(For jar mode only\)

</td>
<td valign="top">

jarPath

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Path to jar to be submitted.

Default: "hdfs://path-to-jar"

</td>
</tr>
<tr>
<td valign="top">

Class Name

\(For jar mode only\)

</td>
<td valign="top">

className

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Name of the class to be executed in jar.

Default: "org.com.smth.className"

</td>
</tr>
<tr>
<td valign="top">

Arguments

\(For jar mode only\)

</td>
<td valign="top">

args

</td>
<td valign="top">

string

</td>
<td valign="top">

Command line arguments for the application.

Default: "arg1,arg2,..."

</td>
</tr>
<tr>
<td valign="top">

Session Name

\(For snippet mode only\)

</td>
<td valign="top">

sessionName

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of this session.

Default: "default session name"

</td>
</tr>
<tr>
<td valign="top">

Code Snippet

\(For snippet mode only\)

</td>
<td valign="top">

snippet

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Snippet of code that has to be submitted.

Default: "snippet of code"

</td>
</tr>
<tr>
<td valign="top">

Snippet Type

\(For snippet mode only\)

</td>
<td valign="top">

snippetType

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Defines the kind of session that should be created for snippet execution \(language of snippet\). Possible values: spark, pyspark, pyspark3 or sparkr.

Default: "spark"

</td>
</tr>
<tr>
<td valign="top">

Strict Snippet Execution Mode

\(For snippet mode only\)

</td>
<td valign="top">

strictSnippetExecutionMode

</td>
<td valign="top">

bool

</td>
<td valign="top">

Mandatory. Defines whether operator is tolerant to errors in snippet execution output, for example, switches strict and not strict modes of snippet submitting.

Default: "false"

</td>
</tr>
</table>



<a name="loiocaf0066d15454d379ef71ad1a157f5bc__section_knq_5f3_vdb"/>

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

`inport` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Accepts path to jar or snippet of code that has to be submitted. Input signal initiates job submitting.

</td>
</tr>
</table>



<a name="loiocaf0066d15454d379ef71ad1a157f5bc__section_swc_cg3_vdb"/>

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

string

</td>
<td valign="top">

The following information will be sent to this port if the submitted job finishes successfully:

-   sourceType `jar`: the corresponding Livy log

-   sourceType `snippet`: output of the executed snippet




</td>
</tr>
<tr>
<td valign="top">

`error` 

</td>
<td valign="top">

string

</td>
<td valign="top">

If the submitted job fails and the Livy operator is using `pipeline` error handling mode, the error will be routed to this port.

</td>
</tr>
</table>

