<!-- loiof0ba7fa014474739a627d9ef537fb613 -->

# Table to Binary

The Table to Binary operator encodes table data in a serialization data format.



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

Output Format

</td>
<td valign="top">

outputFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The serialization format for the output data.

Possible values:

-   CSV

-   JSON
-   JSONLINES
-   Parquet

Default: CSV

</td>
</tr>
<tr>
<td valign="top">

Collect Batches

</td>
<td valign="top">

collectBatches

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Mandatory. Indicates whether the input data shall be collected in batches. If set to *true*, input batches are collected until the last batch is received and only then is the output provided.

If the input does not contain a "com.sap.headers.batch" header and if set to *true*, then the input stream will be collected \(if `streamSize` is not set to *\-1*\) and a single output is generated.

Possible values:

-   true
-   false

Default: false

</td>
</tr>
<tr>
<td valign="top">

Column Separator

</td>
<td valign="top">

colSep

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory if `outputFormat` is *CSV*. The character that shall be used in the output CSV string to separate data columns. \(Visible if `outputFormat` is *CSV*.\)

Default: ,

</td>
</tr>
<tr>
<td valign="top">

Row Separator

</td>
<td valign="top">

rowSep

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory if `outputFormat` is *CSV*. The character that is used in an input CSV string to separate data rows. If set to *OS*, the OS specific line terminator will be used. \(Visible if `outputFormat` is *CSV*.\)

Possible values:

-   CR
-   LF
-   CRLF

Default: LF

</td>
</tr>
<tr>
<td valign="top">

Include Header Row

</td>
<td valign="top">

header

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Mandatory if `outputFormat` is *CSV*. Indicates whether an input CSV string includes a header row containing the column names. \(Visible if `outputFormat` is *CSV*.\)

Possible values:

-   true

-   false

Default: true

</td>
</tr>
<tr>
<td valign="top">

Column Names

</td>
<td valign="top">

colNames

</td>
<td valign="top">

string

</td>
<td valign="top">

A string specifying the column names as a comma separated list. If `header` is set to *true*, this will override the column names specified in the table metadata. \(Visible if `outputFormat` is *CSV*.\)

Default: none

</td>
</tr>
<tr>
<td valign="top">

Decimal Separator

</td>
<td valign="top">

decSep

</td>
<td valign="top">

string

</td>
<td valign="top">

The character that is used in an input CSV string to separate the integer part from the fractional part of a number written in decimal form. \(Visible if `outputFormat` is *CSV*.\)

Default: .

</td>
</tr>
<tr>
<td valign="top">

Escape Character

</td>
<td valign="top">

escapeChar

</td>
<td valign="top">

string

</td>
<td valign="top">

A character that is used in an input CSV string to escape characters that would otherwise be interpreted as having a special function. \(Visible if `outputFormat` is *CSV*.\)

Default: none

</td>
</tr>
<tr>
<td valign="top">

Quoting Character

</td>
<td valign="top">

quoteChar

</td>
<td valign="top">

string

</td>
<td valign="top">

The character that is used in an input CSV string to denote the start and end of a quoted item. Column and row separators will be ignored inside quoted items. \(Visible if `outputFormat` is *CSV*.\)

Default: \`\`

</td>
</tr>
<tr>
<td valign="top">

Quoting Strategy

</td>
<td valign="top">

quoting

</td>
<td valign="top">

string

</td>
<td valign="top">

Used to specify the quoting strategy to be used when a quoting character is provided. The default strategy is `QUOTING_ALL`. We also do provide `QUOTING_MINIMAL` and `QUOTING_NONNUMERIC`. If no quote character is provided, then the quoting strategy will be replaced with `QUOTE_NONE`. A detailed description of the differente quoting strategies can be found in the [official documentation of the CSV Python module](https://docs.python.org/3/library/csv.html#csv.QUOTE_ALL). \(Visible if `outputFormat` is *CSV*.\)

Default: QUOTE\_ALL

</td>
</tr>
<tr>
<td valign="top">

Datetime Format String

</td>
<td valign="top">

dateFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

A string containing a Python format specification for date or datetime values. \(Visible if `outputFormat` is *CSV*.\)

Default: none

</td>
</tr>
<tr>
<td valign="top">

Format

</td>
<td valign="top">

format

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory if `outputFormat` is *JSON*. The format in which data is represented in an input JSON string. \(Visible if `outputFormat` is *JSON*.\)

Possible values:

-   split

-   records
-   index
-   columns
-   values
-   table

Default: records


<table>
<tr>
<th valign="top">

Format

</th>
<th valign="top">

Syntax

</th>
</tr>
<tr>
<td valign="top">

split

</td>
<td valign="top">

\{ "index": \[ <index value\>, ... \], "columns": \[ <column name\>, ... \], "data": <data in `values` format\> \} *where* <index value\>*is an index identifying each data row*

</td>
</tr>
<tr>
<td valign="top">

records

</td>
<td valign="top">

\[ \{ <column name\>: <value\>, ... \}, ... \]

</td>
</tr>
<tr>
<td valign="top">

index

</td>
<td valign="top">

\{ <index value\>: \{ <column name\>: <value\>, ... \}, ... \}

</td>
</tr>
<tr>
<td valign="top">

columns

</td>
<td valign="top">

\{ <column name\>: \{ <index value\>: <value\>, ... \}, ... \}

</td>
</tr>
<tr>
<td valign="top">

values

</td>
<td valign="top">

\[ \[ <value\>, ... \], ... \]

</td>
</tr>
<tr>
<td valign="top">

table

</td>
<td valign="top">

\{ "schema": <schema\>, "data": <data in `records` format\> \} *where* <schema\> *is*: \{ "fields": \[ \{ "name": <column name\>, "type": <column type\> \}, ... \], "primaryKey": \[ <pk column name\>, ... \] \} *where* <column type\> *is one of* "string", "number", "integer", "boolean", "datetime"

</td>
</tr>
</table>



</td>
</tr>
<tr>
<td valign="top">

Compression Type

</td>
<td valign="top">

compression

</td>
<td valign="top">

string

</td>
<td valign="top">

The type of compression that shall be used for the output data. If not specified, no compression will be applied. \(Visible if `outputFormat` is *Parquet*.\)

Possible values:

-   snappy

-   gzip
-   brotli

Default: none

</td>
</tr>
<tr>
<td valign="top">

Partitioning Columns

</td>
<td valign="top">

partitionCols

</td>
<td valign="top">

string

</td>
<td valign="top">

A string containing a comma separated list of column names by which to partition the data. Columns are partitioned in the order they are given. If not specified, no partitioning will be applied. \(Visible if `outputFormat` is *Parquet*.\)

Default: none

</td>
</tr>
</table>



<a name="loiof0ba7fa014474739a627d9ef537fb613__section_knq_5f3_vdb"/>

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

ID

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`table` 

</td>
<td valign="top">

table

</td>
<td valign="top">

\*

</td>
<td valign="top">

Input data table.

</td>
</tr>
</table>



<a name="loiof0ba7fa014474739a627d9ef537fb613__section_swc_cg3_vdb"/>

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

ID

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`binary` 

</td>
<td valign="top">

scalar

</td>
<td valign="top">

com.sap.core.binary

</td>
<td valign="top">

The input table data serialized in the specified format. For the output formats *CSV* and *JSONLINES*, the operator is streaming new line delimited records to the output, while for the other output formats, a processing of the full table at once is required. The opened stream is sending bytes to the consumer, and therefore the consumer has to ensure a proper handling of the stream as incomplete records can be consumed \(for example, streaming byte chunks to a file\). If the consumer relies on complete records, then the consumer can make use of the new line delimiter while consuming the byte stream.

</td>
</tr>
<tr>
<td valign="top">

`error`

</td>
<td valign="top">

scalar

</td>
<td valign="top">

com.sap.error

</td>
<td valign="top">

An error that occurred during the conversion.

</td>
</tr>
</table>

