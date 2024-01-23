<!-- loiofda7323f33584cb0bdd25bc7730d777f -->

# Flowagent Table Producer \(Deprecated\)

Reads from any Flowagent-based consumer operator and writes in a table of any supported database.



This operator is deprecated. We recommend using the [Table Producer V3](table-producer-v3-092de44.md) operator.

Supported databases are:

-   HANA



<a name="loiofda7323f33584cb0bdd25bc7730d777f__section_byb_wbx_cfb"/>

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

Mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Write mode.

-   Append: append to and existing table.

-   Overwrite: drop the table and create another one according to the source schema.

-   Truncate: truncate the table before writing any data.


Default: `"overwrite"`

</td>
</tr>
<tr>
<td valign="top">

Database type

</td>
<td valign="top">

string

</td>
<td valign="top">

The target database to operate. Additional parameters may depend on the selected service.

</td>
</tr>
<tr>
<td valign="top">

Target Table

</td>
<td valign="top">

string

</td>
<td valign="top">

The table where the data will be written. This field accepts two input formats: adapted dataset of the table, which can be selected via the browsing action, or qualified name in `<Schema>.<TableName>` format.

</td>
</tr>
<tr>
<td valign="top">

Column Mapping

</td>
<td valign="top">

object

</td>
<td valign="top">

Defines how the source schema will be mapped to the target schema. It is an array where each element defines a mapping between a column in the source schema to a column in the target schema. If the array is empty, then the default mapping will be equivalent to mirroring the source schema in the target schema.

Mapping use case: You can use mapping to change the order of source columns, or rename them. Example:

```
"mapping": [
  {
      "source": "LOC",
      "target": "LOC"
  },
  {
      "source": "DNAME",
      "target": "TGT_DNAME"
  },
  {
      "source": "DEPTNO",
      "target": "SomeNumberThatWeCareAbout"
  }
]
```



</td>
</tr>
<tr>
<td valign="top">

Source Column Name

</td>
<td valign="top">

string

</td>
<td valign="top">

Column name in the source table.

</td>
</tr>
<tr>
<td valign="top">

Target Column Name

</td>
<td valign="top">

string

</td>
<td valign="top">

Column name in the target table.

</td>
</tr>
<tr>
<td valign="top">

HANA Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a HANA database.

</td>
</tr>
<tr>
<td valign="top">

HDL DB Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

The object containing the connection parameters to a HDL DB database.

</td>
</tr>
<tr>
<td valign="top">

Batch size

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the number of rows that will be inserted in a single commit.

Default: 100

</td>
</tr>
<tr>
<td valign="top">

HDL DB Target Table

</td>
<td valign="top">

object

</td>
<td valign="top">

The HDL DB table where the data is written. This field accepts two input formats: adapted dataset of the table, which can be selected via the browsing action, or qualified name in <Schema\>.<TableName\> format.

</td>
</tr>
</table>



<a name="loiofda7323f33584cb0bdd25bc7730d777f__section_dkd_3y5_whb"/>

## Delta Processing

`Change Data Applier` mode is applicable only with operator that supports DELTA extraction, like ABAP ODP Consumer, Cloud Data Integration Consumer, and so on.


<table>
<tr>
<th valign="top">

Paraneter

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

Change Data Applier Mode

</td>
<td valign="top">

string

</td>
<td valign="top">

The delta record provides a row type like: Insert \(I\), Update \(U\), Delete \(D\), Before Image \(B\), Unknown \(X\), and so on. User can either decide to keep a history of changed records \(Track Change History\), or decide to apply the changes directly to the target \(Apply Change Data\). Currently, only HANA database supports Apply Change Data mode.

Default: "Track Change History"

</td>
</tr>
</table>



<a name="loiofda7323f33584cb0bdd25bc7730d777f__section_s1d_wtw_cfb"/>

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

The source connection information provided by Flowagent-based consumer operator from which data will be read.

</td>
</tr>
</table>



<a name="loiofda7323f33584cb0bdd25bc7730d777f__section_dfm_c5w_cfb"/>

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

`outTableName` 

</td>
<td valign="top">

string

</td>
<td valign="top">

The fully qualified name of the target table.

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

