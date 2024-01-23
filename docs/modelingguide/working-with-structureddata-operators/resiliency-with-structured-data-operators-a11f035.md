<!-- loioa11f035ef8dc43e3815ac63830a0d9c9 -->

# Resiliency with Structured Data Operators

Table Consumer version 3 \(com.sap.database.table.consumer.v3\) is part of the Generation 2 set of operators, and you can run pipelines with snapshot enabled.

Here are the requirements:

-   Table Consumer must be configured with a Partition Type:
    -   *Logical* \(user-defined\) for all supported sources
    -   *Row ID* and *Physical* \(Source Based\) for Oracle

-   Table Consumer must not be in a group with multiplicity greater than one.
    -   Snapshot does not support multiplicity greater than one.
    -   If you want to run partitions in parallel, then snapshot is not supported.


If your pipeline does not meet the requirements above, you can still run the graph. However, snapshot is not enabled.

For more information about partitioning, see [Partitioning](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/86085d9ccd9d49f69464e7c8e6c6f91f.html "Data partitioning separates large datasets into smaller ones based on a set of defined criteria.") :arrow_upper_right:.

For more information about graph termination using partition, see [Graph Termination Using Partition](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/76478fd5bd5a4b709e4b28ad23e71224.html "Learn how to stop a graph with partitions based on the operator generation.") :arrow_upper_right:.



<a name="loioa11f035ef8dc43e3815ac63830a0d9c9__section_cyw_dwn_1rb"/>

## Resiliency Behavior

On restart, the pipeline skips processing partitions that were successfully consumed previously. For example:

In the first run, partitions 1 and 2 were completed successfully, but the graph crashed while running partition 3 and only some rows were read from partition 3. On restart, the pipeline skips partitions 1 and 2 and then starts processing from partition 3.

Different delivery guarantees are provided depending on the producer and writing modes selected. We recommend that you use a combination that leads to **exactly-once** delivery guarantee whenever possible. The table describes the behavior of the Structured Data Producer Operators.


<table>
<tr>
<th valign="top">

Operator

</th>
<th valign="top">

Mode

</th>
<th valign="top">

Delivery Guarantee

</th>
<th valign="top">

Note

</th>
</tr>
<tr>
<td valign="top">

Table Producer

</td>
<td valign="top">

Append + Upsert

</td>
<td valign="top">

exactly-once

</td>
<td valign="top">

No duplicated data in the target.

</td>
</tr>
<tr>
<td valign="top">

Table Producer

</td>
<td valign="top">

Append, Truncate, or Overwrite

</td>
<td valign="top">

at-least-once

</td>
<td valign="top">

Target could have some duplicated data from a partition that was partially run, but it will not lose any data.

</td>
</tr>
<tr>
<td valign="top">

Structured File Producer

</td>
<td valign="top">

Overwrite

</td>
<td valign="top">

exactly-once

</td>
<td valign="top">

There is exactly one file per partition index.

</td>
</tr>
<tr>
<td valign="top">

Structured File Producer

</td>
<td valign="top">

Append

</td>
<td valign="top">

at-least-once

</td>
<td valign="top">

Target could have some duplicated data from a partition that was partially run, but it will not lose any data.

</td>
</tr>
<tr>
<td valign="top">

Structured File Producer

</td>
<td valign="top">

Overwrite or Append + Part-file

</td>
<td valign="top">

exactly-once

</td>
<td valign="top">

Operator ensures that files within a part-file directory are unique per partition index.

</td>
</tr>
<tr>
<td valign="top">

Application Producer

</td>
<td valign="top">

Append

</td>
<td valign="top">

at-least-once

</td>
<td valign="top">

Target could have some duplicated data from a partition that was partially run, but it will not lose any data.

</td>
</tr>
<tr>
<td valign="top">

Cloud Table Producer

</td>
<td valign="top">

Append or Truncate

</td>
<td valign="top">

at-least-once

</td>
<td valign="top">

Target could have some duplicated data from a partition that was partially run, but it will not lose any data.

</td>
</tr>
</table>



<a name="loioa11f035ef8dc43e3815ac63830a0d9c9__section_cm2_2xn_1rb"/>

## Sample Graph

The sample graph com.sap.flowagent.gen2.resilient demonstrates how a resilient pipeline with partition can be modeled.

