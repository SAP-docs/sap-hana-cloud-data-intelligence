<!-- loio03705cd2359c451486eb70469b99f7c6 -->

# Table to Message Converter

The Table to Message Converter operator receives a data type as input and then outputs the data as message content with a CSV body as a string.



This operator is very similar to [Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md) and has the same set of properties.



<a name="loio03705cd2359c451486eb70469b99f7c6__section_hgl_2p2_p2b"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Parameter

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

CSV Properties

</td>
<td valign="top">

additionalProperties\_csv

</td>
<td valign="top">

object

</td>
<td valign="top">

Properties of the CSV content.

-   Column delimiter \(ID `columnDelimiter`, type `string`\): Optional. The field separator. The following characters are supported: `","`, `";"`, `"|"`, `":"`, and `"TAB"`. Default: `","`

-   Text Delimiter Style \(ID `textDelimiterStyle`, type `string`\): Optional. Indicates how the text delimiter should be applied. Always: the text delimiter is added to all columns. Minimal: the text delimiter is added only when necessary. Default: `"Minimal"`
-   Header Included \(ID `csvHeaderIncluded`, type `boolean`\): Optional. Indicates whether each CSV output has a header as the first line. Default: `false`
-   Header Frequency \(ID `csvHeaderIncludedBehavior`, type `string`\): Optional. Indicates when the header is output. First batch: the header is output in the first batch only. Every batch: the header is output for all batches. Default: `"First batch"`



</td>
</tr>
<tr>
<td valign="top">

Batch Size

</td>
<td valign="top">

batchSize

</td>
<td valign="top">

integer

</td>
<td valign="top">

Optional. Indicates the number of rows in each output batch.

Default: `1000`

</td>
</tr>
<tr>
<td valign="top">

Force Batch Size

</td>
<td valign="top">

forceBatchSize

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Use the number defined in the Batch Size option.

Default: `false`

</td>
</tr>
</table>



<a name="loio03705cd2359c451486eb70469b99f7c6__section_f1y_4rh_rrb"/>

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

inTable

</td>
<td valign="top">

table

</td>
<td valign="top">

The source connection information provided by Flowagent-based consumer operator from where the data is read.

</td>
</tr>
</table>



<a name="loio03705cd2359c451486eb70469b99f7c6__section_svg_vrh_rrb"/>

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

outMessage

</td>
<td valign="top">

message

</td>
<td valign="top">

Outputs a message object with the following definition:

-   Body \(type `string`\): CSV formatted data. If the source doesn’t have any rows, it contains an empty string.

-   Attributes
    -   header \(type `string`\): Header of the CSV, when Header Included is set to True.

    -   message.lastBatch \(type `boolean`\): Boolean that indicates that the current batch is the last one.
    -   message.batchIndex \(type `int`\): Number that indicates which batch is being processed, starting from 0.
    -   producer.type \(type `string`\): Type of the producer that generated the message, which can be one of the following depending on which operator generated the message: `CSV` for Flowagent CSV Producer, `File` for Flowagent File Producer, or `Table` for Flowagent Table Producer.
    -   producer.subType \(type `string`\): Subtype of the object that is generated in the target, which can be one of the following: `TABLE`, `CSV`, `PARQUET`, or `ORC` depending on the producer settings.
    -   producer.partition.count \(type `integer`\): Number of partitions from the source.
    -   producer.partition.index \(type `integer`\): Current partition index that was processed. This ranges from 0 to partition.count - 1. See [Graph Termination Using Partition](graph-termination-using-partition-76478fd.md) to learn how to use this information to stop a graph using partitions.

-   Encoding: string



</td>
</tr>
</table>

Check the graph [CSV Producer](../data-intelligence-graphs/csv-producer-055bdbd.md) to check how this port can be used along with a JS Message Operator.

