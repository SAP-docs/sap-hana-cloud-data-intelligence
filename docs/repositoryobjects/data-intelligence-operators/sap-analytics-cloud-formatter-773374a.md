<!-- loio773374a47ec84498a9621d0122d83ceb -->

# SAP Analytics Cloud Formatter

Converts `message.table` input data to message format before sending to SAP Analytics Cloud. Use the SAP Analytics Cloud Formatter operator before the SAP Analytics Cloud Producer operator.



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

Tenant

</td>
<td valign="top">

Tenant

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Enter the SAP Analytics Cloud tenant name where data is pushed.

</td>
</tr>
<tr>
<td valign="top">

Target Dataset

</td>
<td valign="top">

Target Dataset

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The available options are:

-   *Append*: Choose an existing dataset where records are added to existing content.

-   *Replace*: Overwrite all data in an existing dataset.
-   *New*: Create a dataset.


Default: "New"

</td>
</tr>
<tr>
<td valign="top">

Target Dataset ID

</td>
<td valign="top">

Target Dataset ID

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory when the Target Dataset option is set to Append or Replace.

> ### Note:  
> Replace will overwrite all data in a dataset with every request sent to SAC. Adjust Records per Request and Maximum Time in Buffer settings accordingly to prevent data loss.

> ### Note:  
> Find the dataset ID in the SAP Analytics Cloud application by browsing to the desired dataset and extracting the ID from the URL query. For example, the dataset ID is shown in bold in this query:<code>https://SAC_HOST_NAME/sap/fpa/ui/tenants/TENANT_NAME/app.html#;view_id=ds-datasethome;datasetId=<b>123456789ABCDEF</b></code>



</td>
</tr>
<tr>
<td valign="top">

Dataset Name

</td>
<td valign="top">

Dataset Name

</td>
<td valign="top">

string

</td>
<td valign="top">

Required when the *Target Dataset* option is set to *New*. Enter a unique name for a new dataset.

> ### Note:  
> All datasets are created at the root level of your SAP Analytics Cloud file system, where they can be moved from within the SAP Analytics Cloud application.



</td>
</tr>
<tr>
<td valign="top">

Dataset Description

</td>
<td valign="top">

Dataset Description

</td>
<td valign="top">

string

</td>
<td valign="top">

Optional. Enter a description of the dataset contents.

</td>
</tr>
<tr>
<td valign="top">

Input Contains Column Headings

</td>
<td valign="top">

Input Contains Column Headings

</td>
<td valign="top">

bool

</td>
<td valign="top">

Required. The available options are:

-   *True*: Operator uses the input column names as output column names.

-   *False*: Define the output column names in the Output Schema option. You can use this option when the input dataset has column headings. There may be times when you want to change the column headings on output.


Default: "false"

</td>
</tr>
<tr>
<td valign="top">

Output Schema

</td>
<td valign="top">

Output Schema

</td>
<td valign="top">

array

</td>
<td valign="top">

Required when the *Input Contains Column Headings* option is set to *False*.

Define the output columns by clicking the pencil icon. Click *\+* Add. Enter the column name, type, and length. Click *Save*. Repeat for the rest of the columns in the dataset. Use the up and down arrows to move the column names in the order in the dataset.

</td>
</tr>
<tr>
<td valign="top">

Records per Request

</td>
<td valign="top">

Records per Request

</td>
<td valign="top">

integer

</td>
<td valign="top">

Required when the *Target Dataset* option is set to *Append* or *Replace*.

Enter a value greater than 0. The operator attempts to send the specified number of records in one request towards the SAP Analytics Cloud operator. The actual number may be less due to the Maximum Time in Buffer option.

</td>
</tr>
<tr>
<td valign="top">

Maximum Time in Buffer

</td>
<td valign="top">

Maximum Time in Buffer

</td>
<td valign="top">

integer

</td>
<td valign="top">

Required when the *Target Dataset* option is set to *Append* or *Replace*. Time is in milliseconds \(ms\).

Set the value to 0 to send the data immediately. Set the value higher to include more records in the specified batch. For example, when *Records per Request* is set to 1000, and *Maximum Time in Buffer* is set to 10 ms, then the operator may not have enough time to send a batch of 1000 records. Therefore, only a portion of the records is output. If you want the records sent immediately, you might set *Records per Request* to 1 and *Maximum Time in Buffer* to 0.

</td>
</tr>
</table>



<a name="loio773374a47ec84498a9621d0122d83ceb__section_vjb_qh3_zhb"/>

## Request Limits

The SAP Analytics Cloud application imposes these limits.


<table>
<tr>
<th valign="top">

Option

</th>
<th valign="top">

Limit

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

HTTP Request Size

</td>
<td valign="top">

100 MB

</td>
<td valign="top">

Maximum dataset size per HTTP request.

</td>
</tr>
<tr>
<td valign="top">

Row Count

</td>
<td valign="top">

2 Billion

</td>
<td valign="top">

Maximum accumulative dataset row count

</td>
</tr>
<tr>
<td valign="top">

Column Count

</td>
<td valign="top">

1000

</td>
<td valign="top">

Maximum dataset column count

</td>
</tr>
</table>



<a name="loio773374a47ec84498a9621d0122d83ceb__section_pvt_k33_zhb"/>

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

Input

</td>
<td valign="top">

message.table

</td>
<td valign="top">

Table message with records to send to the SAP Analytics Cloud application.

See [Table Messages](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/cf6b74cc9e974981b5bd7400a131ebec.html "A table message is an SAP Data Intelligence Modeler message that represents tabular data. The port type for table messages is message.table.") :arrow_upper_right: for more information on the `message.table` format.

</td>
</tr>
</table>



<a name="loio773374a47ec84498a9621d0122d83ceb__section_kns_t33_zhb"/>

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

Output

</td>
<td valign="top">

Message

</td>
<td valign="top">

Formatted message sent to the SAP Analytics Cloud Producer operator.

</td>
</tr>
</table>

