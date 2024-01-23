<!-- loio1509d8f805844011af971410877ff95b -->

# Avro Decoder

The Avro Decoder operator allows you to decode messages represented in various formats such as Avro, CSV, and JSON for processing in the pipeline.



In this operator, an Avro schema that defines the structure of the record is used. It derives the target table schema and can be included in the message body if the payload body is an Avro message. Otherwise, it can be specified in this operator's configuration or included in the message attributes with the attribute "avro.schema".

The following table describes the supported Avro primitive and logical types and how they are translated into SQL types.

**Type Mapping in Avro, JSON, CSV**


<table>
<tr>
<th valign="top">

Avro

</th>
<th valign="top">

Go

</th>
<th valign="top">

JS

</th>
<th valign="top">

CSV \(sample values\)

</th>
<th valign="top">

SQL

</th>
</tr>
<tr>
<td valign="top">

boolean

</td>
<td valign="top">

bool

</td>
<td valign="top">

bool

</td>
<td valign="top">

true

</td>
<td valign="top">

BOOLEAN

</td>
</tr>
<tr>
<td valign="top">

int

</td>
<td valign="top">

int32

</td>
<td valign="top">

Number

</td>
<td valign="top">

9

</td>
<td valign="top">

INTEGER

</td>
</tr>
<tr>
<td valign="top">

long

</td>
<td valign="top">

int64

</td>
<td valign="top">

Number

</td>
<td valign="top">

"99"

</td>
<td valign="top">

BIGINT

</td>
</tr>
<tr>
<td valign="top">

float

</td>
<td valign="top">

float32

</td>
<td valign="top">

Number

</td>
<td valign="top">

"99.9"

</td>
<td valign="top">

FLOAT

</td>
</tr>
<tr>
<td valign="top">

double

</td>
<td valign="top">

float64

</td>
<td valign="top">

Number

</td>
<td valign="top">

99.99

</td>
<td valign="top">

DOUBLE

</td>
</tr>
<tr>
<td valign="top">

bytes

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

aGVsbG8=

</td>
<td valign="top">

VARCHAR\(\*\)

</td>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

hello

</td>
<td valign="top">

VARCHAR\(\*\)

</td>
</tr>
<tr>
<td valign="top">

decimal\(p,s\)

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

1987.74

</td>
<td valign="top">

DECIMAL\(p,s\)

</td>
</tr>
<tr>
<td valign="top">

date

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

2017-08-29

</td>
<td valign="top">

DATE

</td>
</tr>
<tr>
<td valign="top">

time-millis

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

15:28:50.345

</td>
<td valign="top">

TIME

</td>
</tr>
<tr>
<td valign="top">

time-micros

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

"15:28:50.345678"

</td>
<td valign="top">

TIME

</td>
</tr>
<tr>
<td valign="top">

timestamp-millis

</td>
<td valign="top">

time.Time

</td>
<td valign="top">

string

</td>
<td valign="top">

2017-08-29 15:28:50.345

</td>
<td valign="top">

TIMESTAMP

</td>
</tr>
<tr>
<td valign="top">

timestamp-micros

</td>
<td valign="top">

time.Time

</td>
<td valign="top">

string

</td>
<td valign="top">

2017-08-29 15:28:50.345678

</td>
<td valign="top">

TIMESTAMP

</td>
</tr>
<tr>
<td valign="top">

fixed\(n\)

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

68656c6c6f

</td>
<td valign="top">

VARCHAR\(2n\)

</td>
</tr>
<tr>
<td valign="top">

array

</td>
<td valign="top">

\[\]interface\{\}

</td>
<td valign="top">

array

</td>
<td valign="top">

"\[""paris"",""berlin""\]"

</td>
<td valign="top">

VARCHAR\(\*\)

</td>
</tr>
<tr>
<td valign="top">

map

</td>
<td valign="top">

map\[string\]interface\{\}

</td>
<td valign="top">

object

</td>
<td valign="top">

"\{""france"":""paris"",""germany"":""berlin""\}"

</td>
<td valign="top">

VARCHAR\(\*\)

</td>
</tr>
</table>

> ### Note:  
> aGVsbG8= and 68656c6c6f are the base64 and hexadecimal representations of value hello, respectively.

> ### Note:  
> When you have to store both Array and map Avro types in a single field \(for example: a table column or a CSV field\), they must be represented as the JSON string.

> ### Note:  
> date, time-millis, time-micros, timestamp-millis, and timestamp-micros values can also be represented as an integer-based representation based on the Avro's type definition instead of the above string-based representation.
> 
> **Alternative Time Representation Using Integer Numbers**
> 
> 
> <table>
> <tr>
> <th valign="top">
> 
> Avro
> 
> </th>
> <th valign="top">
> 
> Go
> 
> </th>
> <th valign="top">
> 
> JS
> 
> </th>
> <th valign="top">
> 
> CSV, JS \(sample values\)
> 
> </th>
> </tr>
> <tr>
> <td valign="top">
> 
> date
> 
> </td>
> <td valign="top">
> 
> int64
> 
> </td>
> <td valign="top">
> 
> Number
> 
> </td>
> <td valign="top">
> 
> 17407
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> time-millis
> 
> </td>
> <td valign="top">
> 
> int64
> 
> </td>
> <td valign="top">
> 
> Number
> 
> </td>
> <td valign="top">
> 
> 55730345
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> time-micros
> 
> </td>
> <td valign="top">
> 
> int64
> 
> </td>
> <td valign="top">
> 
> Number
> 
> </td>
> <td valign="top">
> 
> 55730345678
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> timestamp-millis
> 
> </td>
> <td valign="top">
> 
> int64
> 
> </td>
> <td valign="top">
> 
> Number
> 
> </td>
> <td valign="top">
> 
> 1504020530345
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> timestamp-micros
> 
> </td>
> <td valign="top">
> 
> int64
> 
> </td>
> <td valign="top">
> 
> Number
> 
> </td>
> <td valign="top">
> 
> 1504020530345678
> 
> </td>
> </tr>
> </table>

The above Avro to SQL type association may be customized using the extension properties. The following table describes the supported extension properties.

**Extension Attributes for Field**


<table>
<tr>
<th valign="top">

Extension Property

</th>
<th valign="top">

Supported in Avro Types

</th>
<th valign="top">

Property Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

colName

</td>
<td valign="top">

all types

</td>
<td valign="top">

string

</td>
<td valign="top">

Specify the column name.

</td>
</tr>
<tr>
<td valign="top">

size

</td>
<td valign="top">

int

</td>
<td valign="top">

Number

</td>
<td valign="top">

Specify the bit size 8, 16, 32, 64 to use TINYINT, SMALLINT, INTEGER, BIGINT, respectively.

</td>
</tr>
<tr>
<td valign="top">

maxLength

</td>
<td valign="top">

string, bytes

</td>
<td valign="top">

Number

</td>
<td valign="top">

Specify the maximal length.

</td>
</tr>
<tr>
<td valign="top">

primaryKey

</td>
<td valign="top">

all types

</td>
<td valign="top">

bool

</td>
<td valign="top">

Specify whether the field is primary key.

</td>
</tr>
</table>

In addition to the above extension properties applicable to the fields, the following extension properties are applicable to the record level.

**Extension Attributes for Record**


<table>
<tr>
<th valign="top">

Extension Property

</th>
<th valign="top">

Property Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

tableName

</td>
<td valign="top">

string

</td>
<td valign="top">

Specify the table name.

</td>
</tr>
<tr>
<td valign="top">

partitioningCriteria

</td>
<td valign="top">

string

</td>
<td valign="top">

Specify the partitioning criteria \(for example, "HASH \( code \) MIN PARTITIONS 4 MAX PARTITIONS 4" to use a hash partition on field code with size 4.

</td>
</tr>
</table>

A record can be nested arbitrarily, and it is flattened to a fixed table column definition. In the derived table column definition, the column names from a nested record correspond to the fully qualified field names of the record by default \(for instance, each field name in the nested structure is concatenated: a field named *<bar\>* under its parent field named *<foo\>* is named as *<foo\_bar\>*\). Both `array` and `map` fields within a record are serialized into JSON at their corresponding column position.

When using CSV records, records are represented by rows of CSV lines. The first line can represent the field or column names, commonly known as the header line. In this case, the ordering of the fields does not necessarily match the ordering of the fields defined in the Avro schema. Furthermore, some fields can be omitted if there is no value corresponding to those fields. If no header line is present, the ordering of the values must match the ordering of the fields defined in the Avro schema. A value may or may not be enclosed in double quotes. However, a value must be enclosed in double quotes if it contains a special character such as a comma, a double quote, etc. Within the enclosed double quotes, a double quote must be escaped with another double quote [\[RFC-4180\]](https://tools.ietf.org/html/rfc4180).

When using JSON records, records are represented as a JSON array of maps or arrays. The former assumes a map-based representation of a record, where each key-value pair in the map is assigned to its corresponding field. An example of such maps is `[{"city":"madrid","temperature":28.0},{"city":"berlin","temperature":31.0},{"city":"rome","temperature":35.0}]`. The latter assumes the structure similar to CSV, where an array of values is used to represent a record. An example of such arrays is `[["city","temperature"],["madrid",28.0],["berlin",31.0],["rome",35.0]]`. In this case, the first array may represent the optional header line. The JSON records may be given as either a structured object \(that is, as an array of maps or arrays\) or its serialized string form.

The body of the decoded message is an array of records, where each record is an array of Golang typed values.

**Schema Definition Attributes**


<table>
<tr>
<th valign="top">

Property Name

</th>
<th valign="top">

Go Type

</th>
<th valign="top">

JS Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

recName

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

The record name that is used to derive the table name \(for example, "edevice\_record"\)

</td>
</tr>
<tr>
<td valign="top">

tableName

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

The optional table name \(for example, "edevice\_table"\).

</td>
</tr>
<tr>
<td valign="top">

pertitioningCriteria

</td>
<td valign="top">

string

</td>
<td valign="top">

string

</td>
<td valign="top">

The optional partitioning criteria \(for example, "HASH \(code\) MIN PARTITIONS 4 MAX PARTITIONS 4 INTERVAL \(ts\) '10' MINUTE"\)

</td>
</tr>
<tr>
<td valign="top">

fieldNames

</td>
<td valign="top">

\[\]string

</td>
<td valign="top">

string\[\]

</td>
<td valign="top">

The field names \(for example, \["idx", "code", "magnitude", "ts"\]\)

</td>
</tr>
<tr>
<td valign="top">

fieldTypes

</td>
<td valign="top">

\[\]string

</td>
<td valign="top">

string\[\]

</td>
<td valign="top">

The field types in golang type \(for example, \["int", "string", "double", "timestamp-millis"\]\)

</td>
</tr>
<tr>
<td valign="top">

fieldNillables

</td>
<td valign="top">

\[\]bool

</td>
<td valign="top">

boolean\[\]

</td>
<td valign="top">

The field nillables \(for example, \[false, false, false, false\]\)

</td>
</tr>
<tr>
<td valign="top">

fieldDefaultss

</td>
<td valign="top">

\[\]interface\{\}

</td>
<td valign="top">

any\[\]

</td>
<td valign="top">

The field default \(for example, \[nil, "xxx", 50.0, nil\]\)

</td>
</tr>
<tr>
<td valign="top">

fieldPrimaryKeys

</td>
<td valign="top">

\[\]bool

</td>
<td valign="top">

boolean\[\]

</td>
<td valign="top">

The field primary keys \(for example, \[true, false, false, true\]\)

</td>
</tr>
<tr>
<td valign="top">

colNames

</td>
<td valign="top">

\[\]string

</td>
<td valign="top">

string\[\]

</td>
<td valign="top">

The table column names \(for example, \["idx", "code", "magnitude", "ts"\]

</td>
</tr>
<tr>
<td valign="top">

colTypes

</td>
<td valign="top">

\[\]string

</td>
<td valign="top">

string\[\]

</td>
<td valign="top">

The table column types \(for example, \["INTEGER", "VARCHAR\(25\)", "DOUBLE", "TIMESTAMP"\]

</td>
</tr>
</table>

If the body of the decoded message is modified or rearranged, the above metadata must be adjusted to match the modified body.



<a name="loio1509d8f805844011af971410877ff95b__section_sq1_nf3_vdb"/>

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

Default Avro Schema

</td>
<td valign="top">

defaultAvroSchema

</td>
<td valign="top">

string

</td>
<td valign="top">

The default Avro schema to be used when the incoming message does not include its schema. This parameter is mandatory for Avro messages without schema, CSV, or JSON messages.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Variable Limit

</td>
<td valign="top">

varLimit

</td>
<td valign="top">

integer

</td>
<td valign="top">

The default size limit for the varchar columns, where 0 indicates unlimited, that is, '\*'.

Default: 0

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

The input message format. The accepted values are "avro", "csv", or "json".

Default: "avro"

</td>
</tr>
<tr>
<td valign="top">

Use Schema Registry

</td>
<td valign="top">

useSchemaRegistry

</td>
<td valign="top">

bool

</td>
<td valign="top">

The input Avro message contains the schema ID whose corresponding schema is stored at some schema registry. Note the schema itself needs to be retrieved offline and set to parameter `defaultAvroSchema`.

Default: false

</td>
</tr>
<tr>
<td valign="top">

CSV Comma

</td>
<td valign="top">

csvComma

</td>
<td valign="top">

rune

</td>
<td valign="top">

The delimiter character code for the CSV format. For example, 44 for ','; 59 for ';'; 124 for '|'.

Default: ,

</td>
</tr>
<tr>
<td valign="top">

CSV Header Included

</td>
<td valign="top">

csvHeaderIncluded

</td>
<td valign="top">

bool

</td>
<td valign="top">

The input CSV message contains the header line.

Default: false

</td>
</tr>
</table>



<a name="loio1509d8f805844011af971410877ff95b__section_knq_5f3_vdb"/>

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

`in` 

</td>
<td valign="top">

message

</td>
<td valign="top">

Accepts messages containing Avro, CSV, or JSON messages in the body.

</td>
</tr>
</table>



<a name="loio1509d8f805844011af971410877ff95b__section_swc_cg3_vdb"/>

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

`error` 

</td>
<td valign="top">

message

</td>
<td valign="top">

If this port is not connected, any processing error will lead to the termination of the operator. If this port is connected, a message containing the original header attributes \(that is, all except `message.commit.token` and an additional attribute `message.response.error` set to the error\) and the body payload is emitted from this port.

</td>
</tr>
</table>

