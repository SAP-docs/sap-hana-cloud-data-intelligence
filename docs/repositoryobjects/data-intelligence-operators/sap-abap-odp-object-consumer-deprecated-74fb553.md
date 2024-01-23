<!-- loio74fb55330a5d4912ac1ea5072579198f -->

# SAP ABAP ODP Object Consumer \(Deprecated\)

Reads from an ABAP ODP object.



It uses Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator \(for example, [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)\).



> ### Restriction:  
> This operator is deprecated and will be removed soon.
> 
> Please use its successor [ABAP ODP Reader](abap-odp-reader-d4c18f8.md).
> 
> Refer to SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



<a name="loio74fb55330a5d4912ac1ea5072579198f__section_sq1_nf3_vdb"/>

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

ABAP Connection \(protocol RFC only\)

</td>
<td valign="top">



</td>
<td valign="top">



</td>
</tr>
<tr>
<td valign="top">

ODP Object

</td>
<td valign="top">

string

</td>
<td valign="top">

ODP Object \(for example, `/EXTRACTORS/<ODP Context>/<Extractor Name>`\).

</td>
</tr>
<tr>
<td valign="top">

Trace Level

</td>
<td valign="top">

string

</td>
<td valign="top">



</td>
</tr>
<tr>
<td valign="top">

Fetch Size

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the number of rows that will be fetched from the source in each request. For wide tables, smaller values are better. For tables with fewer columns, larger values are better.

Default: 100

</td>
</tr>
</table>



<a name="loio74fb55330a5d4912ac1ea5072579198f__section_zk4_p2b_xhb"/>

## ODP Filters

After importing the ODP source, you can also edit the filters in the UI. During metadata import, the source will provide the type of filters available or possible operators for each column.

User will need to select the column, choose the operator \(`=` or `BETWEEN`\) then provide the values.

The filters will be applied during the graph run. Filters is available in both mode, `FULL` or `DELTA`.



<a name="loio74fb55330a5d4912ac1ea5072579198f__section_bw5_t2b_xhb"/>

## Delta Processing

ODP object can provide delta records in different ways. The delta record will provide a row type like Insert \(I\), Update \(U\), Delete \(D\), Before Image \(B\), Unknown \(X\) etc. User can either decide to keep a history of changed records \(`Track Change History`\) mode, or decide to apply the changes directly to the target \(`Apply Change Data`\) mode. These options are exposed on the operators that support such feature.

By default, Flowagent CSV and File producer support only `Track Change History mode`, while Flowagent Table Producer with HANA as selected service, will support both modes. For HANA Table Producer, user can select `Apply Change Data` in the applier type, this will cause Flowagent to apply the changes to the target table, so I,U,D will properly be applied to the target.

Based on your extractor source type, you can either use `Track Change History` mode to keep a history or changed records or Apply Change Data mode to apply these delta changes to the target system. Below lists some of the ODP Object types and their support in Delta + `Apply Change Data` support.


<table>
<tr>
<th valign="top">

Delta Type

</th>
<th valign="top">

Description

</th>
<th valign="top">

Apply Change Data Support

</th>
</tr>
<tr>
<td valign="top">

ADD

</td>
<td valign="top">

Additive Extraction \(for example, LIS Info Structures\)

</td>
<td valign="top">

Not supported with HANA Producer in Apply Change Data Mode. All delta rows will be ignored

</td>
</tr>
<tr>
<td valign="top">

AIE

</td>
<td valign="top">

After-Images \(FI-GL/AP/AR\)

</td>
<td valign="top">

Delete is not send by the source, hence target data won't get deleted.

</td>
</tr>
<tr>
<td valign="top">

AIED

</td>
<td valign="top">

After-Images with Deletion Flag \(FI-GL/AP/AR\)

</td>
<td valign="top">

Supported.

</td>
</tr>
<tr>
<td valign="top">

NEWE

</td>
<td valign="top">

Only New Records \(Inserts\) \(Cube-Compatible\)

</td>
<td valign="top">

Supported.

</td>
</tr>
<tr>
<td valign="top">

ODS

</td>
<td valign="top">

ODS Extraction

</td>
<td valign="top">

Supported.

</td>
</tr>
</table>



<a name="loio74fb55330a5d4912ac1ea5072579198f__section_djs_kfb_xhb"/>

## Delta Columns

ABAP ODP consumer add the following columns to the original table.


<table>
<tr>
<th valign="top">

Column Name

</th>
<th valign="top">

Description

</th>
<th valign="top">

Source

</th>
</tr>
<tr>
<td valign="top">

DI\_SEQUENCE\_NUMBER

</td>
<td valign="top">

Contains an integer for sequencing.

</td>
<td valign="top">

ODP Consumer Operator

</td>
</tr>
<tr>
<td valign="top">

DI\_OPERATION\_TYPE

</td>
<td valign="top">

Contains the row operation type: I \(insert\), D \(delete\), X \(unknown\), and the sort.

</td>
<td valign="top">

ODP Consumer Operator

</td>
</tr>
<tr>
<td valign="top">

ODQ\_CHANGEMODE

</td>
<td valign="top">

For CDC, identifies the row type. Works in conjunction with ODQ\_ENTITYCNTR to determine how to handle the row. C \(create\), U \(update\), D \(delete\).

</td>
<td valign="top">

SAP

</td>
</tr>
<tr>
<td valign="top">

ODQ\_ENTITYCNTR

</td>
<td valign="top">

For CDC, an integer that works in conjunction with ODQ\_CHANGEMODE to determine how to the handle row.

</td>
<td valign="top">

SAP

</td>
</tr>
</table>

The following table describes the relationships between ODQ\_CHANGEMODE and ODQ\_ENTITYCNTR.


<table>
<tr>
<th valign="top">

CHANGEMODE

</th>
<th valign="top">

ENTITYCNTR

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

C

</td>
<td valign="top">

\+1

</td>
<td valign="top">

The record is new and inserted.

</td>
</tr>
<tr>
<td valign="top">

U

</td>
<td valign="top">

\+1

</td>
<td valign="top">

The record is inserted.If there is a record with same key already available, the record is updated. In this case, there should be a corresponding U- \(short notation for U and -1\) record. The record contains the new information.

</td>
</tr>
<tr>
<td valign="top">

U

</td>
<td valign="top">

\-1

</td>
<td valign="top">

The record is deleted and replaced with the corresponding record with same key and U+ \(short notation for U and +1\) if available. The record contains the previous \(old or outdated\) information.

</td>
</tr>
<tr>
<td valign="top">

U

</td>
<td valign="top">

0

</td>
<td valign="top">

The record is updated, but the key figures must be added to the already available key figures. So the record returns the difference between the old record and the new record, not the new record itself.

</td>
</tr>
<tr>
<td valign="top">

D

</td>
<td valign="top">

\-1

</td>
<td valign="top">

The record is deleted. It contains the same key as an already existing record, but the key figures are inverted. So the record might be "deleted" by adding the key figures to the already available values. They should sum up to 0.

</td>
</tr>
<tr>
<td valign="top">

D

</td>
<td valign="top">

\+1

</td>
<td valign="top">

The record is deleted. It contains the actual data in both key and key figures.

</td>
</tr>
</table>



<a name="loio74fb55330a5d4912ac1ea5072579198f__section_qkb_kgb_xhb"/>

## Delta Recovery

In case of graph failures or recovery, user can get the composite request id from ODQ Monitor \(`/odqmon`\) and choosing the subscription id they have provided during the graph creation. The composite request id is a timestamp of job last ran, user can then edit the graph and provide the value in the "Extraction from Timestamp" field to signal the timestamp where Flowagent should read the records from.

> ### Note:  
> Only in case of `Apply Change Data` mode, the data will be consistent with source system. In case of `Track Change History` the target can contain duplicate records.



<a name="loio74fb55330a5d4912ac1ea5072579198f__section_knq_5f3_vdb"/>

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

`inTableName` 

</td>
<td valign="top">

string

</td>
<td valign="top">

ODP object name \(for example, `/EXTRACTORS/<ODP Context>/<Extractor Name>`\).

> ### Note:  
> This is optional. If ODP Object Name is presented, this port is ignored.



</td>
</tr>
</table>



<a name="loio74fb55330a5d4912ac1ea5072579198f__section_swc_cg3_vdb"/>

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

`outConfig` 

</td>
<td valign="top">

string.flowagent.config

</td>
<td valign="top">

Flowagent type port, which only `Flowagent producers` can consume \(for example, Flowagent File Producer\). In order to get the data as string, `Flowagent CSV Producer`can be used as producer.

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

Operator error. If mapped, the operator error is sent to the operator this port is mapped to and the graph remains running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

