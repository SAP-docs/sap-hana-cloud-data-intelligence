<!-- loioc25dff36e88346b9916e9f3e0800605a -->

# SAP HANA Client

Executes SQL statements and inserts CSV or JSON data into an SAP HANA instance. It supports three fundamental operations:



-   **Executing arbitrary SQL code**:

    SQL code arrives at port `sql`.

    When executing stored procedures with a `CALL` statement, please note that only scalar output parameters are supported.

-   **Executing prepared statements**:

    A message arrives at port `data` with the `hana.preparedStatement` attribute, which names one of the prepared statement configured in *Prepared statements* to be executed. The message body must be of type:

    -   `[][]interface{}`;

    -   `[]interface{}`\) containing `[]interface{}`;

    -   `[][]string`, in case all statement parameters accept strings;

    -   `[][]float64`, in case all statement parameters accept integers or floating-point; or

    -   `nil`, in which case the prepared statement is executed without arguments.


    If the body is none of the above types, an error is raised.

    Also, placeholders of the following datatypes are not currently supported for prepared statement executions:

    `DECIMAL`, `SMALLDECIMAL`, and all `DATETIME` types listed in the **Supported Types** \> **Insertion** section below.

-   **Inserting data into a predefined table**:

    A message arrives at port `data` **without** the `hana.preparedStatement` attribute. The message body is parsed as either CSV or JSON \(see *Input format*\) and the resulting rows are inserted into the table identified by *Table name*, according to the column names and types in *Table columns*.

    You can use a single HANA Client operator to perform all three operations, because the input ports work independently from one another.




<a name="loioc25dff36e88346b9916e9f3e0800605a__section_sq1_nf3_vdb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Title

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

Connection

</td>
<td valign="top">

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. The object containing the connection parameters to a HANA instance.

> ### Note:  
> It may be necessary to enable TLS in your connection configuration. Error messages such as `i/o timeout`, `connection reset by peer` and `EOF` may indicate that a network firewall is dropping insecure packets.

When TLS is enabled, the operator uses the "Validate hostname in certificate" \(`hostnameInCertificate`\) connection property for the TLS Server Name extension. If this property is empty, the operator falls back to `host`, which must be a hostname and not an IP address.

Default: \{\}

</td>
</tr>
<tr>
<td valign="top">

Output in Batches

</td>
<td valign="top">

outputInBatches

</td>
<td valign="top">

bool

</td>
<td valign="top">

Determines whether output messages should be broken by the number of rows specified in *Output batch size*. If enabled, output messages resulting from queries contain the standard set of batching attributes, except for the optional `message.batchCount`.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Output Batch Size

</td>
<td valign="top">

outputBatchSize

</td>
<td valign="top">

integer

</td>
<td valign="top">

The number of rows that should be placed in each output message when executing queries. This value is used only when *Output in batches* is true and it must be an integer greater than zero.

Default: 10

</td>
</tr>
<tr>
<td valign="top">

Init Statements

</td>
<td valign="top">

initStatements

</td>
<td valign="top">

string

</td>
<td valign="top">

The SQL statements are executed immediately after the graph starts, independent of any input data and without producing any output data. The statements are executed after *Table Initialization*. Placing a HANA Client operator inside a group with multiplicity larger than 1 causes these initialization statements to be executed multiple times.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Prepared Statements

</td>
<td valign="top">

preparedStatements

</td>
<td valign="top">

array

</td>
<td valign="top">

A JSON array of SQL statements. Those statements are prepared during operator initialization and can be invoked using the `hana.preparedStatement` message attribute for port `data`.

For efficient insertion, prefer `BULK INSERT` over regular `INSERT`, because the latter inserts rows one by one whereas the former batches them to reduce network usage. Note that `BULK INSERT` statements without arguments \(question-mark placeholders\) produce no effect.

Default: \[\]

</td>
</tr>
<tr>
<td valign="top">

Table Name

</td>
<td valign="top">

tableName

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the table to insert data into. If empty, port `data` can receive only messages with the `hana.preparedStatement` attribute. Refer to the *Case Sensitivity* section below for applicable naming rules.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Table Columns

</td>
<td valign="top">

tableColumns

</td>
<td valign="top">

array

</td>
<td valign="top">

An array describing the columns of the table identified by *Table name*. If empty, port `data` can receive only messages with the `hana.preparedStatement`attribute. Refer to the *Case Sensitivity* section below for applicable naming rules.

The *size*, *precision* and *scale* fields are used only if *Table Initialization* is not `None`.

Default: \[\]

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

Mandatory. The format used to parse the data received at the `data` port.

Accepted values are:

-   `CSV`: input is broken into records using *CSV record delimiter*; records are broken into fields using *CSV field delimeter*. Each field is parsed according to the type defined for its column in *Table columns*.

-   `JSON`: input must come as a JSON array. Each of its elements can be either:

    -   a JSON array representing a table row; its elements must be in the same order as *Table columns*;

    -   a JSON object whose keys are the column names in *Table columns*; spare keys are ignored.


    When using JSON, each column value is treated in its JSON-native type, unconverted.


Default: "CSV"

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

Specifies how the operator should interpret the CSV data that arrives at the `data` port for insertion \(without the `hana.preparedStatement` attribute\). Accepted values:

-   `Batch`: Each chunk from the input is parsed as a self-contained CSV string. The records are inserted before reading the next input from `data`.

-   `Stream`: Each chunk is considered as the next piece of a single stream, so each input doesn't need to be complete. Once **CSV bulk size** records are buffered \(or **CSV bulk timeout** milliseconds go by without any new records\), they are inserted into the table in a single bulk, and an output message is sent to **result** \(if applicable\). After each complete set of batches \(last input containing the `message.lastBatch` attribute\), the operator also sends an additional output message with the `message.lastBatch` attribute to notify that it finished processing all the previously received data. When the graph stops, the stream is ended, so all buffered records are inserted, even if fewer than **CSV bulk size**, and output is not produced. Note that the end of the stream may truncate the last record, so if it was not complete \(had fewer fields than required\), it is discarded, the error is logged, and the pending records that came before are inserted as usual.

> ### Note:  
> The end of the stream may truncate the last record. So if it was not complete \(had fewer fields than required\), it is discarded, the error is logged, and the pending records that came before are inserted as usual.

Default: Batch

</td>
</tr>
<tr>
<td valign="top">

CSV Bulk Size

</td>
<td valign="top">

csvBulkSize

</td>
<td valign="top">

int

</td>
<td valign="top">

When in CSV stream mode, this property determines how many CSV records should be accumulated to be inserted in a single bulk.

Default: 100

</td>
</tr>
<tr>
<td valign="top">

CSV Bulk Timeout

</td>
<td valign="top">

csvBulkTimeoutMs

</td>
<td valign="top">

int

</td>
<td valign="top">

When in CSV stream mode, if this value is positive and no new record was received for this duration, all buffered records are inserted as a bulk.

Default: 10000

</td>
</tr>
<tr>
<td valign="top">

CSV Empty Field Value

</td>
<td valign="top">

csvEmptyFieldValue

</td>
<td valign="top">

string

</td>
<td valign="top">

When input is in CSV format, this property specifies how empty fields are interpreted for string-like columns: `VARCHAR`, `ALPHANUM`, and `SHORTTEXT`. Accepted values are `"NULL"` or `"Empty string"`. For all other colump types, empty CSV fields are converted to the `NULL`

value.

Default: "Empty string"

</td>
</tr>
<tr>
<td valign="top">

CSV Record Delimiter

</td>
<td valign="top">

csvBreak

</td>
<td valign="top">

string

</td>
<td valign="top">

The character used as record delimiter in CSV input. If set to "\\n", both LF and CRLF are accepted.

Default: "\\n"

</td>
</tr>
<tr>
<td valign="top">

CSV Field Delimiter

</td>
<td valign="top">

csvComma

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

CSV Quote Character

</td>
<td valign="top">

csvQuote

</td>
<td valign="top">

string

</td>
<td valign="top">

The character used as quote.

Default: """

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

If true, allows fields to contain unescaped quotes. With this option, your field need only be quoted if its value starts with a literal quote.

**Single-field examples and how to encode them with and without lazy quotes**


<table>
<tr>
<th valign="top">

Desired Value

</th>
<th valign="top">

CSV

</th>
<th valign="top">

CSV \(lazy quotes\)

</th>
</tr>
<tr>
<td valign="top">

ab"

</td>
<td valign="top">

"ab"""

</td>
<td valign="top">

ab"

</td>
</tr>
<tr>
<td valign="top">

a"b

</td>
<td valign="top">

"a""b"

</td>
<td valign="top">

a"b

</td>
</tr>
<tr>
<td valign="top">

"ab

</td>
<td valign="top">

"""ab"

</td>
<td valign="top">

""ab"

</td>
</tr>
<tr>
<td valign="top">

"ab"

</td>
<td valign="top">

"""ab"""

</td>
<td valign="top">

""ab"""

</td>
</tr>
</table>

In the last example with lazy quotes, the second literal quote has to be escaped lest it is regarded as a close-quote due to it being at the end of a quoted field.

Default: true

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

The character used as comment indicator. When this configuration is non-empty, lines starting with this character are ignored.

Default: ""

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

Determines whether CSV contains a header and how to use it. The header is regarded as being the first record of each input \(in `batch` mode\) or of the entire lifetime \(in `stream` mode\).

Accepted values are:

-   `None`: The first record is regular data, not a header.
-   `Ignore`: The first record is a header that should be discarded.
-   `Use as schema`: The first record is a header from which to extract column names. These names are matched against the table schema as reported by `HANA` so that spare columns in the CSV are ignored and missing ones will have a `NULL` value. In this mode, *Table columns* is not used for insertion \(but may still be required by the *Table initialization* option\).

Default: "None"

</td>
</tr>
<tr>
<td valign="top">

Insert Mode

</td>
<td valign="top">

insertMode

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Specifies whether the `INSERT` or the `UPSERT` command should be used for inserting data. When using `UPSERT`, the target table **must** have a primary key. For other uses of `UPSERT`, such as `WHERE` clauses, use *Prepared statements*.

Default: "INSERT"

</td>
</tr>
<tr>
<td valign="top">

Table Initialization

</td>
<td valign="top">

initTable

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Determines whether and how the table from the configuration should be initialized. Requires parameter *Table name* and *Table columns*. It is executed immediately after the graph starts, independent of any input data and without producing any output data and before *Init Statements*. If different than `None`, it ensures the schema exists \(if explicitly given in *Table name*\).

Accepted values are:

-   `None`: no table initialization is done.
-   `Create`: ensures table exists.
-   `Truncate`: ensures table exists and is empty, truncating the table.
-   `Delete Rows`: ensures table exists and is empty, deleting all rows.
-   `Drop` \(Cascade\): ensures table exists and is empty, dropping table with `cascade` option.
-   `Drop` \(Restrict\): ensures table exists and is empty, dropping table with `restrict` option.

Default: "None"

</td>
</tr>
<tr>
<td valign="top">

Table Type

</td>
<td valign="top">

tableType

</td>
<td valign="top">

string

</td>
<td valign="top">

If *Table initialization* is not "None", this option determines whether to create a row or column table.

Default: "Column"

</td>
</tr>
<tr>
<td valign="top">

Decimal Output Format

</td>
<td valign="top">

decimalOutputFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

Determines how the operator should output the values `DECIMAL`- and `SMALLDECIMAL`-type columns.

Accepted values are:

-   `Fraction (string)`: Decimals are the form `<numerator>/<denominator>` in a string.
-   `Floating-point`: Decimals are converted to double precision floating-point numbers. The resulting number may not represent the exact value of the division.

Default: "Fraction \(string\)"

</td>
</tr>
<tr>
<td valign="top">

Transaction Level

</td>
<td valign="top">

transactionLevel

</td>
<td valign="top">

string

</td>
<td valign="top">

When running SQL statements with the `sql` input, this option determines how the operator groups statements into database transactions.

Accepted values:

-   Per statement: a separate transaction is used for each statement.

-   Per input: a separate transaction is used for each input, and each transaction encompasses all statements in that input.

Default: "Per statement"

</td>
</tr>
<tr>
<td valign="top">

Network Batch Size \(rows\)

</td>
<td valign="top">

networkBatchSize

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of rows to fetch from the server in each batch when executing queries. This value can be adjusted to affect the granularity of network requests the operator performs.

Default: 512

</td>
</tr>
<tr>
<td valign="top">

Connection Timeout \(ms\)

</td>
<td valign="top">

connectionTimeoutInMs

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of milliseconds to wait for in each network operation:

-   establishing the connection
-   receiving query results
-   sending data

All communication with the server is broken down into packets of at most 4KiB. The timeout applies to the reading and writing of each such packet. The value zero disables the timeout and allows operations to run indefinitely.

Default: 50000

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

bool

</td>
<td valign="top">

A flag that indicates whether or not the graph should stop if this operator encounters an error. If set to `false`, an output may represent an error, in which case its attribute `message.error` is `true` and its body contains a string describing the error.

> ### Note:  
> This setting **does not apply** to errors during initialization, such as compiling *Prepared statements* or executing the *Init statements*. In such cases, errors always cause the graph to fail.

Default: true

</td>
</tr>
</table>



<a name="loioc25dff36e88346b9916e9f3e0800605a__section_knq_5f3_vdb"/>

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

`sql` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Accepts SQL code in a message's body to be executed by the `SAP HANA` instance.

</td>
</tr>
<tr>
<td valign="top">

`data` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Accepts CSV or JSON data in a message's body. If the attribute `hana.preparedStatement` is present, its value is used to identify a prepared statement to which this data is submitted \(see *Executing prepared statements* for the accepted data format\). Otherwise, data is inserted into the table identified by *Table name*.

</td>
</tr>
</table>



<a name="loioc25dff36e88346b9916e9f3e0800605a__section_swc_cg3_vdb"/>

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

A message containing the result of an operation. The original input message attributes are preserved in the output, except when in CSV stream mode, because the output is decoupled from the input. If the operation retrieved rows, they are in the message body as an array of objects. Each key in an object is the uppercase name of the corresponding table column.

</td>
</tr>
</table>



<a name="loioc25dff36e88346b9916e9f3e0800605a__section_xrv_xxw_vdb"/>

## Supported Types



### Insertion

The following data types are supported by this operator when using the `data` port:

-   Numeric Types
    -   `TINYINT`
    -   `SMALLINT`
    -   `INTEGER`
    -   `BIGINT`
    -   `FLOAT`
    -   `DOUBLE`
    -   `DECIMAL` and `SMALLDECIMAL`. These values must be represented as:
        -   a number in decimal notation \(for example, `4.12`, `23`\); or

        -   a fraction of the form `<numerator>/denominator>` \(for example, `43/10`\).

            In JSON, they can be either a string in one of the above formats \(for example, `[[1.3], ["2.1"], ["3/4"]]` is a valid input to insert three rows into a decimal-type column.



-   Boolean Type:
    -   `BOOLEAN`

-   Character String Types:
    -   `VARCHAR`
    -   `NVARCHAR`

-   Datetime Types: the following types are supported, along with HANA's default format for each of them:
    -   `DATE: YYYY-MM-DD (for example, '1957-06-13')`
    -   `TIME: HH24:MI:SS (for example, '23:32:18')`
    -   `TIMESTAMP: YYYY-MM-DD HH24:MI:SS.FF7 (for example, '1957-06-13 23:32:18.8261933')`
    -   `SECONDDATE: YYYY-MM-DD HH24:MI:SS (for example, '1957-06-13 23:32:18')`




### Querying

When a query is sent to port `sql`, the type of each value in the output matches the table below.


<table>
<tr>
<th valign="top">

Column Type

</th>
<th valign="top">

Output Type

</th>
</tr>
<tr>
<td valign="top">

`TINYINT,SMALLINT, INTEGER, BIGINT`

</td>
<td valign="top">

`int64`

</td>
</tr>
<tr>
<td valign="top">

`FLOAT, REAL, DOUBLE`

</td>
<td valign="top">

`float64`

</td>
</tr>
<tr>
<td valign="top">

`DECIMAL, SMALLDECIMAL`

</td>
<td valign="top">

See *Decimal output format*

</td>
</tr>
<tr>
<td valign="top">

`ALPHANUM, SHORTTEXT, VARCHAR, NVARCHAR`

</td>
<td valign="top">

`string`

</td>
</tr>
<tr>
<td valign="top">

`SECONDDATE`

</td>
<td valign="top">

`string ("YYYY-mm-dd HH:MM:SS")`

</td>
</tr>
<tr>
<td valign="top">

`TIMESTAMP`

</td>
<td valign="top">

`string ("YYYY-mm-dd HH:MM:SS.NNNNNNN")`

</td>
</tr>
<tr>
<td valign="top">

`DATE`

</td>
<td valign="top">

`string ("YYYY-mm-dd")`

</td>
</tr>
<tr>
<td valign="top">

`TIME`

</td>
<td valign="top">

`string ("HH:MM:SS")`

</td>
</tr>
<tr>
<td valign="top">

`BOOLEAN`

</td>
<td valign="top">

`int64 (0 or 1)`

</td>
</tr>
<tr>
<td valign="top">

`VARBINARY, TEXT, BLOB, CLOB, NCLOB`

</td>
<td valign="top">

`[]byte`

</td>
</tr>
</table>

`NULL` values are always output as `nil`, regardless of the column type.

> ### Note:  
> Due to internal technical limitations, `CALL` statements that have output parameters do not yet obey the table above, except for integer, floating-point, and boolean types.



<a name="loioc25dff36e88346b9916e9f3e0800605a__section_x54_cph_53b"/>

## Case Sensitivity

Identifiers in SAP HANA are case-insensitive by default, so they are implicitly capitalized. When written in double-quotes, however, they become case-sensitive and must always be spelled exactly the same as when they were created. When using this operator, you must take case sensitivity into account: If a schema, table, or column was created using quotes, then its name in the operator's configuration must also be in quotes and in the same case.

The snippet below shows some examples and explanations on case sensitivity:

```
-- Because we're not using quotes, mySchema will be capitalized: MYSCHEMA.
CREATE SCHEMA mySchema;

-- myTable, B and c are all case-sensitive.
CREATE TABLE MYSCHEMA."myTable" (A INTEGER, "B" VARCHAR(1), "c" TIMESTAMP);

-- This statement will run successfully because b is not in quotes, so it
-- will be capitalized, becoming B, which is the correct name of the column.
INSERT INTO myschema."myTable" (a, b, "c") VALUES (0, 'x', NOW());

-- This statement will fail because c has to be quoted and lowercase.
INSERT INTO myschema."myTable" (a, b, c) VALUES (1, 'y', NOW());
```

