<!-- loio8dc583223dae450e8691fa2532c2a4d5 -->

# Structured File Consumer V2

Structured File Consumer operator reads from any supported cloud storage. This operator is supported in Generation 1 graphs.



The operator produces structured output, and you need to connect it to other operators from Structured Data Operators category, for example, [Data Transform V2](data-transform-v2-a415f61.md) or [Structured File Producer V3](structured-file-producer-v3-605e08a.md).

> ### Caution:  
> Support for Microsoft Azure Data Lake Storage Gen1 \(ADL\) in this operator is deprecated.

The supported cloud storages include the following:

-   Microsoft Azure Data Lake Storage V2 \(ADL\_V2\)
-   Google Cloud Storage \(GCS\)
-   Hadoop Distributed File System \(HDFS\)
-   SAP HANA Data Lake Files \(HDL\_FILES\)
-   Alibaba Cloud Object Storage Service \(OSS\)
-   Amazon Simple Storage Service \(S3\)
-   Semantic Data Lake \(SDL\)
-   Microsoft Azure Storage Blob \(WASB\)



<a name="loio8dc583223dae450e8691fa2532c2a4d5__section_sq1_nf3_vdb"/>

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

Storage type

</td>
<td valign="top">

string

</td>
<td valign="top">

The storage from which the file is read. Additional parameters may depend on the selected cloud storage.

</td>
</tr>
<tr>
<td valign="top">

Source Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Connection ID of the source system.

</td>
</tr>
<tr>
<td valign="top">

Source Object

</td>
<td valign="top">

object

</td>
<td valign="top">

Remote dataset of the selected file.

</td>
</tr>
<tr>
<td valign="top">

Fail on string truncation

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Indicates whether the reader should exit and fail if a string truncation has happened. This behavior happens when the length of a string in the metadata is smaller than the actual data in the source file.

</td>
</tr>
<tr>
<td valign="top">

Maximum Fetch Size

</td>
<td valign="top">

integer

</td>
<td valign="top">

The maximum number of records from the source included in each batch. The actual number of records is automatically calculated based on the dataset definition. To disable the automatic calculation, set the Use Defined Fetch Size option to True.

</td>
</tr>
<tr>
<td valign="top">

Use Defined Fetch Size

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Set to True when the automatic calculation doesn’t provide optimal performance. When set to True, each batch of records contains the number of records entered in the Maximum Fetch Size option. For example, when Maximum Fetch Size is set to 1000, and Use Defined Fetch Size is set to True, then there are 1000 records in each batch. When set to False, then each batch is between 10 and 1000 rows.

</td>
</tr>
</table>



<a name="loio8dc583223dae450e8691fa2532c2a4d5__section_chg_p3d_qnb"/>

## Remote Source Description Limitation

The UI obtains the metadata definition for the file after you select a file to be read via the browsing UI. Consider the following:

-   CSV files do not have a metadata definition, so the application infers the metadata by looking at the file. The column properties like delimiter, escape character, text delimiter, and charset can be modified in case the inference is wrong.
-   Parquet and ORC files have a metadata definition, but they do not specify the length of strings, which default to 5000.
-   JSON/JSONL files column definitions default to string\(5000\) for arrays and structures when not flattened. The flattening level property is used to control the level of flattening and can be modified to any level below the maximum value for modeling. Modifying the flattening level updates the metadata definition and the data preview.
-   Supported Excel files include XLS \(versions up to 97/2000/XP/2003\) and XLSX with file sizes below **50MB**. You can select only one of the sheets in the file to import.

Given these facts, the metadata can be wrong, and the job can fail. For strings, the default is to fail the job on strings truncation. However, the operator can be configured to tolerate string truncations by setting the **Fail on string truncation** property to **false**.



<a name="loio8dc583223dae450e8691fa2532c2a4d5__section_hxr_2f1_k4b"/>

## Custom Editor

This operator uses a custom editor user interface. See [Custom Editor](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/8cda7c3a4ab74c86ba5752456418c4b0.html "Use the Custom Editor to update the source dataset and projection and filters are pushed down to the source.") :arrow_upper_right:.



<a name="loio8dc583223dae450e8691fa2532c2a4d5__section_knq_5f3_vdb"/>

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

inTrigger

</td>
<td valign="top">

message

</td>
<td valign="top">

Trigger to indicate that the operator should start the execution.

> ### Note:  
> The input port is optional. If the input port does not have a connection, then the operator starts when the graph starts running.



</td>
</tr>
</table>



<a name="loio8dc583223dae450e8691fa2532c2a4d5__section_swc_cg3_vdb"/>

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

outTable

</td>
<td valign="top">

table

</td>
<td valign="top">

Table type port, which can be used to connect to other structured operators.

</td>
</tr>
</table>

**Related Information**  


[Custom Editor](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/8cda7c3a4ab74c86ba5752456418c4b0.html "Use the Custom Editor to update the source dataset and projection and filters are pushed down to the source.") :arrow_upper_right:

