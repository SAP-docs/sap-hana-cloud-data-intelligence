<!-- loio9de323a9941d4d3092ca445497bbd1a8 -->

# SAP HANA Monitor

This operator watches a HANA table and outputs newly inserted rows as a message.



It works by creating a trigger on the table to copy each inserted row into a temporary table. The temporary table is periodically queried and cleared so that it contains the new rows since the last poll. No output is produced if there were no new rows since the last query.



<a name="loio9de323a9941d4d3092ca445497bbd1a8__section_sq1_nf3_vdb"/>

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

Connection

</td>
<td valign="top">

Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. The object containing the connection parameters to a HANA instance.

> ### Note:  
> it may be necessary to enable TLS in your connection configuration. Error messages such as `i/o timeout`, `connection reset by peer` and `EOF` may indicate that a network firewall is dropping insecure packets

When TLS is enabled, the operator uses the "Validate hostname in certificate" \(`hostnameInCertificate`\) connection property for the TLS Server Name extension. If this property is empty, the operator falls back to `host`, which must be a hostname and not an IP address.

</td>
</tr>
<tr>
<td valign="top">

Schema name

</td>
<td valign="top">

Schema name

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The schema of the monitored table.

Default: "

</td>
</tr>
<tr>
<td valign="top">

Table name

</td>
<td valign="top">

Table name

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The table to be monitored.

Default: "

</td>
</tr>
<tr>
<td valign="top">

Table columns

</td>
<td valign="top">

Table columns

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. A comma-separated list of column names and types. Sized types \(such as VARCHAR and FLOAT\) must include their sizes in parentheses. For example:

```
ID INTEGER, NAME VARCHAR(64), WAGE DECIMAL(11,2)
```

Default: "

</td>
</tr>
<tr>
<td valign="top">

Poll period

</td>
<td valign="top">

Poll period

</td>
<td valign="top">

int

</td>
<td valign="top">

Mandatory.

The time in milliseconds on which the temporary table will be polled for new rows.

Default: 1000

</td>
</tr>
<tr>
<td valign="top">

Connection timeout

</td>
<td valign="top">

Connection timeout

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of milliseconds to wait for when connecting to HANA before timing out.

Default: 10000

</td>
</tr>
</table>



<a name="loio9de323a9941d4d3092ca445497bbd1a8__section_knq_5f3_vdb"/>

## Input

None.



<a name="loio9de323a9941d4d3092ca445497bbd1a8__section_swc_cg3_vdb"/>

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

`outResult` 

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose body contains the new rows as an array of objects. Each key in an object is the uppercase name of the corresponding table column.

</td>
</tr>
</table>

