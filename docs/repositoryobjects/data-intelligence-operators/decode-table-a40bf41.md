<!-- loioa40bf411b6d64a4a9cd4c226a7ad52aa -->

# Decode Table

This operator decodes tabular data from one of the supported formats into table messages. Currently, only CSV input is supported.



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

Input Format

</td>
<td valign="top">

format

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Determines the format of the input. Currently, only CSV is supported.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

CSV Mode

</td>
<td valign="top">

csvMode

</td>
<td valign="top">

string

</td>
<td valign="top">

When using CSV format, this specifies how the operator should interpret the incoming data.

Accepted values:

-   Batch: each chunk from the input will be parsed as a self-contained CSV string. The records will be inserted before reading the next input from data.

-   Stream: each chunk is considered as the next piece of a single stream, so each individual input does not need to be complete. Once CSV stream bulk size records are buffered \(or CSV stream bulk timeout goes by without any new records\), they are output in a single message. When the graph stops, accumulated records are discarded.

Default: "Batch"

</td>
</tr>
<tr>
<td valign="top">

CSV Stream Bulk Size

</td>
<td valign="top">

csvStreamBulkSize

</td>
<td valign="top">

int

</td>
<td valign="top">

When in CSV stream mode, this property determines how many CSV records should be accumulated to be output in a single message. The value zero makes the bulk unlimited in size, so that records are only output every time the timeout is reached.

Default: 100

</td>
</tr>
<tr>
<td valign="top">

CSV Stream Bulk Timeout

</td>
<td valign="top">

csvStreamBulkTimeout

</td>
<td valign="top">

string

</td>
<td valign="top">

When in CSV stream mode, this option forces the operator to output all accumulated records, even if there are less than the bulk size \(CSV stream bulk size\). The value zero disables the timeout, so records are only flushed when the bulk size is reached.

Default: "10s"

</td>
</tr>
<tr>
<td valign="top">

CSV Field Delimiter

</td>
<td valign="top">

csvFieldDelimiter

</td>
<td valign="top">

string

</td>
<td valign="top">

The character used as field delimiter in CSV input.

Default: ","

</td>
</tr>
<tr>
<td valign="top">

CSV Comment Character

</td>
<td valign="top">

csvComment

</td>
<td valign="top">

string

</td>
<td valign="top">

The character used as comment indicator. When this configuration is non-empty, lines starting with this character will be ignored.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

CSV Lazy Quotes

</td>
<td valign="top">

csvLazyQuotes

</td>
<td valign="top">

bool

</td>
<td valign="top">

If true, allows fields to contain unescaped quotes. With this option, only quotes at the start of a field need to be escaped.

Default: true

</td>
</tr>
<tr>
<td valign="top">

CSV Header

</td>
<td valign="top">

csvHeader

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines whether CSV will contain a header and how to use it. The header will be regarded as being the first record of each input \(in batch mode\) or of the entire lifetime \(in stream mode\).

Accepted values:

-   None: the first record is regular data, not a header.

-   Ignore: the first record is a header that should be discarded.
-   Column names: the first record is a header from which to extract column names. These names will be stored in Table Message’s standard `table.columns` attribute.

Default: "None"

</td>
</tr>
</table>



<a name="loioa40bf411b6d64a4a9cd4c226a7ad52aa__section_ckt_g13_rrb"/>

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

input

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose body will be decoded according to the `Input Format` configuration.

</td>
</tr>
</table>



<a name="loioa40bf411b6d64a4a9cd4c226a7ad52aa__section_exd_k13_rrb"/>

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

output

</td>
<td valign="top">

message.table

</td>
<td valign="top">

A table message holding the data decoded from the input. The original input message attributes will be preserved in the output, except when in CSV stream mode, since output is decoupled from input.

</td>
</tr>
</table>

