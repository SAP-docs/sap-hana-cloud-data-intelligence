<!-- loio1bb16c01874b4b2c9916c323d758f74f -->

# Binary to Table V2

The Binary to Table operator decodes serialized data and provides the data in table format.



<a name="loio1bb16c01874b4b2c9916c323d758f74f__section_sq1_nf3_vdb"/>

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

Table Name

</td>
<td valign="top">

inputFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

A name for the input table data. If not specified the path of the input file will be used as table name.

Default: none

</td>
</tr>
<tr>
<td valign="top">

Input Format

</td>
<td valign="top">

inputFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The serialization format of the input data.

Possible values:

-   CSV
-   JSON
-   JSONLINES
-   Parquet
-   ORC

Default: CSV

</td>
</tr>
<tr>
<td valign="top">

Output Batches

</td>
<td valign="top">

outputBatches

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Mandatory. Indicates whether the output data shall be provided in batches.

Possible values:

-   true

-   false

Default: false

</td>
</tr>
<tr>
<td valign="top">

Batch Size \(Rows\)

</td>
<td valign="top">

batchSize

</td>
<td valign="top">

integer

</td>
<td valign="top">

The size of output batches \(specified as a number of rows\) if `outputBatches` is set to *true*.

Default: none

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

Mandatory if `inputFormat` is *CSV*. The character that is used in an input CSV string to separate data columns. If set to *unknown* the operator will try to detect the used column separator. \(Visible if `inputFormat` is *CSV*.\)

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

Mandatory if `inputFormat` is *CSV*. The character that is used in an input CSV string to separate data rows. If set to *OS* the OS specific line terminator will be used. \(Visible if `inputFormat` is *CSV*.\)

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

Mandatory if `inputFormat` is *CSV*. Indicates whether an input CSV string includes a header row containing the column names. \(Visible if `inputFormat` is *CSV*.\)

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

A string specifying the column names as a comma-separated list. If `header` is set to *true*, this will override the column names specified in the header row of the file. If the Table Output has a static vtype, this configuration is ignored and the column names will always be the names of the vtype columns. \(Visible if `inputFormat` is *CSV*.\)

Default: none

</td>
</tr>
<tr>
<td valign="top">

Values for Boolean True

</td>
<td valign="top">

trueValues

</td>
<td valign="top">

string

</td>
<td valign="top">

A string specifying one value, or a comma separated list of values, that shall be interpreted as boolean *true*. \(Visible if `inputFormat` is *CSV*.\)

Default: none

</td>
</tr>
<tr>
<td valign="top">

Values for Boolean False

</td>
<td valign="top">

falseValues

</td>
<td valign="top">

string

</td>
<td valign="top">

A string specifying one value, or a comma separated list of values, that shall be interpreted as boolean *false*. \(Visible if `inputFormat` is *CSV*.\)

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

The character that is used in an input CSV string to separate the integer part from the fractional part of a number written in decimal form. \(Visible if `inputFormat` is *CSV*.\)

Default: .

</td>
</tr>
<tr>
<td valign="top">

Thousands Separator

</td>
<td valign="top">

digitGrpSep

</td>
<td valign="top">

string

</td>
<td valign="top">

A character that is used in an input CSV string to separate groups of digits of a number representing a factor of thousand in front of the decimal separator. \(Visible if `inputFormat` is *CSV*.\)

Default: none

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

A character that is used in an input CSV string to escape characters that would otherwise be interpreted as having a special function. \(Visible if `inputFormat` is *CSV*.\)

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

The character that is used in an input CSV string to denote the start and end of a quoted item. Column and row separators will be ignored inside quoted items. \(Visible if `inputFormat` is *CSV*.\)

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

Used to specify the quoting strategy to be used when a quoting character is provided. The default strategy is QUOTING\_ALL. We also do provide QUOTING\_MINIMAL and QUOTING\_NONNUMERIC. If no quote character is provided then the quoting strategy will be replaced with QUOTE\_NONE. A detailed description of the different quoting strategies can be found in the official documentation of the CSV Python module [here](https://docs.python.org/3/library/csv.html#csv.QUOTE_ALL). \(Visible if `outputForma`t is *CSV*.\)

</td>
</tr>
<tr>
<td valign="top">

Datetime Columns

</td>
<td valign="top">

dateCols

</td>
<td valign="top">

string

</td>
<td valign="top">

A string containing a comma separated list of column names that shall be parsed as date or datetime values. \(Visible if `inputFormat` is *CSV*, *JSON*, *JSONLINES*.\)

Default: none

</td>
</tr>
<tr>
<td valign="top">

Ignore Bad Lines

</td>
<td valign="top">

ignoreBad

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Indicates whether to ignore lines in an input CSV string that contain too many columns. If set to *true*, bad lines will be dropped from the output, otherwise an error will be raised. \(Visible if `inputFormat` is *CSV*.\)

Default: false

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

Mandatory if `inputFormat` is *JSON*. The format in which data is represented in an input JSON string. \(Visible if `inputFormat` is *JSON*.\)

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
</table>



<a name="loio1bb16c01874b4b2c9916c323d758f74f__section_knq_5f3_vdb"/>

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

`binary` 

</td>
<td valign="top">

scalar

</td>
<td valign="top">

com.sap.core.binary

</td>
<td valign="top">

Input serialized data. Can be consumed as a stream by this operator if the `inputFormat` is set to *CSV* or *JSONLINES*. Other formats do not support streaming.

</td>
</tr>
</table>



<a name="loio1bb16c01874b4b2c9916c323d758f74f__section_swc_cg3_vdb"/>

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

`table` 

</td>
<td valign="top">

table

</td>
<td valign="top">

\*

</td>
<td valign="top">

The input serialized data converted to a table sent as a stream.

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

