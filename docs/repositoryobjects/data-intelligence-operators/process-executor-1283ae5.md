<!-- loio1283ae5991fc444cbbdf1c23c8893449 -->

# Process Executor

The Process Executor operator starts a process and provides given contiguous streams to it. The operator finishes when the forked process terminates. A non-zero return code is propagated as an abnormal operator termination.



<a name="loio1283ae5991fc444cbbdf1c23c8893449__section_sq1_nf3_vdb"/>

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

Command Line

</td>
<td valign="top">

cmdLine

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The command line to be executed.

</td>
</tr>
<tr>
<td valign="top">

Output stderr to trace

</td>
<td valign="top">

TraceStderr

</td>
<td valign="top">

bool

</td>
<td valign="top">

Offers the option to send the stderr output of the process also sent to the Modeler trace of the process. The errors are sent as INFO traces with a prepended `[PROC STDERR]`.

Default: false

</td>
</tr>
</table>

If the operator is used as a base operator to define an extended operator, there are two additional options, which are available in the operator editor:


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

code language

</td>
<td valign="top">

codelanguage

</td>
<td valign="top">

string

</td>
<td valign="top">

If the executable is a script, this indicates the programming language used.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

script

</td>
<td valign="top">

script

</td>
<td valign="top">

string

</td>
<td valign="top">

This parameter is not shown in the list with the other configuration parameters, but has a separate tab offering the script editor. The script can be either defined as inline script or a file can be used. In the latter case, the operator configuration later shows `"file://"` as the script file to be executed.

Default: ""

</td>
</tr>
</table>



<a name="loio1283ae5991fc444cbbdf1c23c8893449__section_knq_5f3_vdb"/>

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

`stdin` 

</td>
<td valign="top">

stream

</td>
<td valign="top">

The contiguous stream to be provided on standard input of the forked process.

</td>
</tr>
</table>



<a name="loio1283ae5991fc444cbbdf1c23c8893449__section_swc_cg3_vdb"/>

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

`stdout` 

</td>
<td valign="top">

stream

</td>
<td valign="top">

The contiguous stream arriving from standard output of the forked process.

</td>
</tr>
<tr>
<td valign="top">

`stderr` 

</td>
<td valign="top">

stream

</td>
<td valign="top">

The contiguous stream arriving from standard error of the forked process.

</td>
</tr>
</table>

