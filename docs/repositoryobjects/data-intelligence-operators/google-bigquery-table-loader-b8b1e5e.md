<!-- loiob8b1e5ef2cee48b4ab7aca778348d349 -->

# Google BigQuery Table Loader

This operator writes to a Google BigQuery table.



The Google BigQuery Table Loader operator uses the Flowagent subengine to connect to Google BigQuery. You can either specify the full path of source Google Cloud Storage file in the operator’s configuration or connect any file producer that outputs full path of Google Cloud Storage file to the input of the operator.



<a name="loiob8b1e5ef2cee48b4ab7aca778348d349__section_hfs_4tf_h4b"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Parameter

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

Google BigQuery Connection

</td>
<td valign="top">

Object

</td>
<td valign="top">

Object containing the connection parameters to a Google BigQuery database.

</td>
</tr>
<tr>
<td valign="top">

Source File

</td>
<td valign="top">

String

</td>
<td valign="top">

Full path name of the source Google Cloud Storage file.

</td>
</tr>
<tr>
<td valign="top">

Source file type

</td>
<td valign="top">

String

</td>
<td valign="top">

File type of the source Google Cloud Storage file. Options are CSV, PARQUET, ORC, NEWLINE\_DELIMITED\_JSON, and AVRO.

</td>
</tr>
<tr>
<td valign="top">

Column delimiter

</td>
<td valign="top">

String

</td>
<td valign="top">

Delimiter used for columns in the source file. This option is available for CSV file types.

</td>
</tr>
<tr>
<td valign="top">

Target table name

</td>
<td valign="top">

String

</td>
<td valign="top">

The fully qualified name of and existing target table to which content is written in <owner\>.<table\> or owner/table format. The schema of target table must match the schema of source Google Cloud Storage file.

</td>
</tr>
<tr>
<td valign="top">

Mode

</td>
<td valign="top">

String

</td>
<td valign="top">

Table load mode. Options are Append and Truncate.

</td>
</tr>
</table>



<a name="loiob8b1e5ef2cee48b4ab7aca778348d349__section_pty_hm5_fnb"/>

## Input


<table>
<tr>
<th valign="top">

Parameter

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

inSourceName

</td>
<td valign="top">

String

</td>
<td valign="top">

Full path name of Google Cloud Storage file, it can be overwritten by Source name property, so the port is used as a trigger of the operator.

</td>
</tr>
</table>



<a name="loiob8b1e5ef2cee48b4ab7aca778348d349__section_p31_rm5_fnb"/>

## Output


<table>
<tr>
<th valign="top">

Parameter

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

outTableName

</td>
<td valign="top">

String

</td>
<td valign="top">

The fully qualified name of target table to which content is written.

</td>
</tr>
<tr>
<td valign="top">

outError

</td>
<td valign="top">

String

</td>
<td valign="top">

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

