<!-- loioc5b81c724d0b4000afd1afad214f111e -->

# Format Converter

The Format Converter operator converts blobs between CSV, JSON and XML. The output format is set as a configuration value. The input format is deduced using the following rules:



The input format is deduced using the following rules:

-   If it starts with \{ or \[, it must be JSON.

-   If it starts with <, it must be XML.

-   Otherwise, it must be CSV.


If the first field in CSV input starts with any of the three special characters \(\{, \[ and <\), it must be quoted.



<a name="loioc5b81c724d0b4000afd1afad214f111e__section_jt3_l5c_12b"/>

## CSV

The CSV format conforms to [RFC 4180](https://tools.ietf.org/html/rfc4180), with the following observations:

-   Any valid UTF-8 character or escape sequence may be used as field separator \("comma"\).

-   Output CSV will use CRLF as a record separator, placing it after every record including the last one.

-   Input CSV can use either LF or CRLF as a record separator, and the last record may or may not be followed by a separator.

-   Because CSV lacks any type information, when converting to JSON, all fields will be made into strings.




<a name="loioc5b81c724d0b4000afd1afad214f111e__section_onk_55c_12b"/>

## XML

Converting to XML requires one of the following to be true:

-   xmlOutputRootTag is not empty, in which case all input content will be placed within this tag. For example, input

    ```
    [{"a": 1}, {"b": "hello"}]
    ```

    becomes

    ```
    <root>
        <item>
            <a>1</a>
        </item>
        <item>
            <b>hello</b>
        </item>
    </root>
    ```

    where `xmlOutputRootTag` is root and `xmlOutputItemTag` is item.

-   Input is a JSON object containing a single property, whose key will be used as root tag. For example:

    ```
    {"countries": [{"id": "US", "currency": "USD"}, {"id": "DE", "currency": "EUR"}]}
    ```

    becomes

    ```
    <countries>
        <country>
            <id>US</id>
            <currency>USD</currency>
        </country>
        <country>
            <id>DE</id>
            <currency>EUR</currency>
        </country>
    </countries>
    ```

    assuming `xmlOutputRootTag` is empty and `xmlOutputItemTag` is country.


Converting from XML requires no XML-specific configuration. Sibling tags with the same name will be placed in an array named after them. For example:

```
<people>
    <person>
        <name>Bonnie</name>
        <age>23</age>
    </person>
    <person>
        <name>Clyde</name>
        <age>25</age>
    </person>
</people>
```

will be turned into

```
{
    "people": {
        "person": [
            {"name": "Bonnie", "age": "23"},
            {"name": "Clyde", "age": "25"}
        ]
    }
}
```

Notice that all textual values in XML become JSON strings.



<a name="loioc5b81c724d0b4000afd1afad214f111e__section_sq1_nf3_vdb"/>

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

csvComma



</td>
<td valign="top">

string

</td>
<td valign="top">

The field separator.

Default: ","

</td>
</tr>
<tr>
<td valign="top">

targetFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

The file type to be converted to. Accepted values are JSON, CSV or XML.

Default: "JSON"

</td>
</tr>
<tr>
<td valign="top">

csvHeaderIncluded

</td>
<td valign="top">

bool

</td>
<td valign="top">

Indicates whether or not each CSV input will have a header as first line. If the header will not be present, the fields parameter must be supplied.

Default: false

</td>
</tr>
<tr>
<td valign="top">

fields

</td>
<td valign="top">

string

</td>
<td valign="top">

A comma-separated list of field names. This value is required only when:

-   converting from headerless CSV

-   converting to CSV


Default: " "

</td>
</tr>
<tr>
<td valign="top">

xmlOutputRootTag

</td>
<td valign="top">

string

</td>
<td valign="top">

The name for the root tag to be used when converting to XML. If this value is empty, the operator will be able only to convert JSON input, which must be an object with a single property that will serve as root tag.

Default: "items"

</td>
</tr>
<tr>
<td valign="top">

xmlOutputItemTag

</td>
<td valign="top">

string

</td>
<td valign="top">

The tag name to be used for each element in an array when converting to XML. If this value is empty, xmlOutputRootTag will be used.

Default: "item"

</td>
</tr>
</table>



<a name="loioc5b81c724d0b4000afd1afad214f111e__section_knq_5f3_vdb"/>

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

`input` 

</td>
<td valign="top">

blob

</td>
<td valign="top">

The source data to be converted.

</td>
</tr>
</table>



<a name="loioc5b81c724d0b4000afd1afad214f111e__section_swc_cg3_vdb"/>

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

`output` 

</td>
<td valign="top">

blob

</td>
<td valign="top">

The resulting data, in `targetFormat` format.

</td>
</tr>
</table>

