<!-- loioeb59df89570445e7b09d39a7b6d334b0 -->

# Flowagent CSV Producer

Reads any Flowagent-based consumer operator and outputs in a CSV format conforming to the RFC-4180 specification. The row delimiter is CRLF, the escape character and text delimiter are double quotes, and supported column delimiters include: , ; | : and \\t.



<a name="loioeb59df89570445e7b09d39a7b6d334b0__section_hgl_2p2_p2b"/>

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

Batch Size

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the number of rows that will be presented in each output batch.

Default: 100

</td>
</tr>
<tr>
<td valign="top">

Format

</td>
<td valign="top">

string

</td>
<td valign="top">

Output file format.

Default: "CSV"

</td>
</tr>
<tr>
<td valign="top">

Column Delimiter

</td>
<td valign="top">

char

</td>
<td valign="top">

The field separator. Only the following characters are supported: , ; | : and TAB.

Default: `,`

</td>
</tr>
<tr>
<td valign="top">

Row Delimiter \(user defined\)

</td>
<td valign="top">

string

</td>
<td valign="top">

Indicates a user-defined row delimiter.

</td>
</tr>
<tr>
<td valign="top">

Null Value Replacement

</td>
<td valign="top">

string

</td>
<td valign="top">

Value that will be used to replace null fields.

</td>
</tr>
<tr>
<td valign="top">

Text Delimiter

</td>
<td valign="top">

char

</td>
<td valign="top">

Indicates which character will be used to delimit columns in a row.

Default: `"`

</td>
</tr>
<tr>
<td valign="top">

Text Delimiter Style

</td>
<td valign="top">

string

</td>
<td valign="top">

Indicates how the text delimiter should be applied. If Always is selected, all columns will have a text delimiter; if Minimal, the text delimiter will be added only when necessary.

Default: `Minimal`

</td>
</tr>
<tr>
<td valign="top">

Escape Character

</td>
<td valign="top">

char

</td>
<td valign="top">

Indicates which escape character will be used to escape the text delimiter.

Default: "

</td>
</tr>
<tr>
<td valign="top">

Header Included

</td>
<td valign="top">

bool

</td>
<td valign="top">

Indicates whether or not each CSV output will have a header as first line.

Default: false

</td>
</tr>
</table>



<a name="loioeb59df89570445e7b09d39a7b6d334b0__section_jgl_2p2_p2b"/>

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

`inConfig` 

</td>
<td valign="top">

string.flowagent.config

</td>
<td valign="top">

To be connected to flowagent based consumer operator.

</td>
</tr>
</table>



<a name="loioeb59df89570445e7b09d39a7b6d334b0__section_lgl_2p2_p2b"/>

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

`outContent` 

</td>
<td valign="top">

string

</td>
<td valign="top">

CSV formatted data. If source has no rows, it will contain an empty string.

</td>
</tr>
<tr>
<td valign="top">

`outMessage` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Outputs a message object with the following definition:

-   `Body` \(type string\): CSV-formatted data. If source has no rows, it will contain an empty string.

-   Attributes:
    -   `header` \(type string\): header of the CSV, if header included is true.

    -   `message.lastBatch` \(type boolean\): boolean that indicates if the current batch is the last one.

    -   `message.batchIndex` \(type integer\): number that indicates which batch is being processed, starting from 0.


-   Encoding: `string`


See the graph `com.sap.dh.ingestion.csvproducer` to check how this port can be used along with a JS Message operator.

</td>
</tr>
<tr>
<td valign="top">

`outError` 

</td>
<td valign="top">

string

</td>
<td valign="top">

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

