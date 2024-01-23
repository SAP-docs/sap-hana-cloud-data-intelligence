<!-- loio34cad34027cf4a6a9cfa525c819f462b -->

# Trace Severity Levels

When streaming the traces for the SAP Data Intelligence Modeler application, you can set a trace severity threshold. Depending on the trace level that you define, the application streams messages accordingly into the trace server.



The application supports the following trace levels.


<table>
<tr>
<th valign="top">

Trace Level

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

INFO

</td>
<td valign="top">

The publisher streams trace messages that contain informational text, mostly for echoing what has happened in the application. The trace messages streamed also include messages associated with warnings, errors, and fatal errors.

</td>
</tr>
<tr>
<td valign="top">

DEBUG

</td>
<td valign="top">

The publisher streams trace messages that contain useful information for developers to debug and analyze the application. The trace messages streamed also include messages associated with info, error, warning, and fatal error.

</td>
</tr>
<tr>
<td valign="top">

ERROR

</td>
<td valign="top">

The publisher streams trace messages that contain information describing the error conditions that may occur when working with the application. The trace messages streamed also include messages associated with the fatal error.

</td>
</tr>
<tr>
<td valign="top">

FATAL

</td>
<td valign="top">

The publisher streams trace messages associated with fatal errors that may occur when working with the application.

</td>
</tr>
<tr>
<td valign="top">

WARNING

</td>
<td valign="top">

The publisher streams messages associated with warnings and errors that may occur when working with the application. The trace messages streamed also include messages associated with error and fatal error.

</td>
</tr>
</table>

