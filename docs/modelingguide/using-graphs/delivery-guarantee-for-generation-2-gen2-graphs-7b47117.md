<!-- loio7b471176ba7d490085178d20204efe00 -->

# Delivery Guarantee for Generation 2 \(Gen2\) Graphs

When you enable automatic graph recovery and snapshots for a Gen2 graph \(pipeline\), your graphs can outlast system failures and system maintenance events.

SAP Data Intelligence doesn't persist snapshots continually. Therefore, some already-processed information can be lost, and the Modeler has to reprocess some of the same information after restoring a graph. Regardless, SAP Data Intelligence provides guarantees on the data consistency when there's a chance of losing data or duplicating data when the Modeler recovers the graph.

The following table lists the guarantees that Gen2 graphs with automatic graph recovery and snapshots provide. For descriptions of terms, see [Terminology](delivery-guarantee-for-generation-2-gen2-graphs-7b47117.md#loio7b471176ba7d490085178d20204efe00__section_b3l_h1k_rvb).


<table>
<tr>
<th valign="top">

Source

</th>
<th valign="top">

Batch

</th>
<th valign="top">

Writer

</th>
<th valign="top">

Other Conditions

</th>
<th valign="top">

Guarantee

</th>
</tr>
<tr>
<td valign="top">

Replayable

</td>
<td valign="top">

No

</td>
<td valign="top">

Idempotent

</td>
<td valign="top">

Pipeline is deterministic

</td>
<td valign="top">

Exactly once

</td>
</tr>
<tr>
<td valign="top">

Replayable

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Idempotent

</td>
<td valign="top">

Pipeline is deterministic

Discard duplicate messages after source

</td>
<td valign="top">

Exactly once

</td>
</tr>
<tr>
<td valign="top">

Any

</td>
<td valign="top">

No

</td>
<td valign="top">

Transactional

</td>
<td valign="top">

None

</td>
<td valign="top">

Exactly once

</td>
</tr>
<tr>
<td valign="top">

Replayable

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Transactional

</td>
<td valign="top">

None

</td>
<td valign="top">

Exactly once

</td>
</tr>
<tr>
<td valign="top">

Nonreplayable

</td>
<td valign="top">

No

</td>
<td valign="top">

None

</td>
<td valign="top">

Any

</td>
<td valign="top">

At most once

</td>
</tr>
<tr>
<td valign="top">

Nonreplayable

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Any

</td>
<td valign="top">

Any

</td>
<td valign="top">

At most once

</td>
</tr>
<tr>
<td valign="top">

Replayable

</td>
<td valign="top">

Any

</td>
<td valign="top">

Any

</td>
<td valign="top">

Any

</td>
<td valign="top">

At least once

</td>
</tr>
</table>



<a name="loio7b471176ba7d490085178d20204efe00__section_b3l_h1k_rvb"/>

## Terminology

The terms in this section define the content of the values in the guarantee table.



### Source

A source is an operator that generates data independently of any signal from an input port or ports. The following table describes the values in the Source column.


<table>
<tr>
<td valign="top">

**Replayable**

</td>
<td valign="top">

Data generated at time “T + x” always contains the data that was generated previously, at moment “T”, and in the same order.

The following scenarios apply to replayable generators without batches:

-   Reading immutable file.
-   Query `SELECT ...FROM SALESORDER WHERE ORDERDATE <'10-02-2010' ORDER BY ORDERDATE"`, where the comparison guarantees to always include previous information.
-   Reading from an event queue starting from an offset.
-   Query `"SELECT ...FROM SALESORDER...ORDER BY ORDERDATE"`, where the table is append-only and records can be ordered.



</td>
</tr>
<tr>
<td valign="top">

**Nonreplayable**

</td>
<td valign="top">

Data generated when replayable conditions aren't met.

> ### Note:  
> SAP Data Intelligence reads from a directory of files so that when there's a recovery, it doesn't have to start from the beginning.



</td>
</tr>
<tr>
<td valign="top">

**Any**

</td>
<td valign="top">

Either replayable or nonreplayable.

</td>
</tr>
</table>



### Batch

Data generated and broken into batches. You configure batches typically in the operator configuration.


<table>
<tr>
<td valign="top">

**Yes**

</td>
<td valign="top">

Data is broken into batches.

</td>
</tr>
<tr>
<td valign="top">

**No**

</td>
<td valign="top">

Data isn't broken into batches.

</td>
</tr>
<tr>
<td valign="top">

**Any**

</td>
<td valign="top">

Data is either broken into batches or not.

</td>
</tr>
</table>



### Writer

The writer column contains information about operators that send data outside the graph. The following table describes values in the Writer column.


<table>
<tr>
<td valign="top">

**Idempotent**

</td>
<td valign="top">

Writing data multiple times has the same effect as writing data once. An idempotent writer can be guaranteed by the operator's operation, such as an UPSERT or a write-ahead log \(WAL\).

</td>
</tr>
<tr>
<td valign="top">

**Transactional**

</td>
<td valign="top">

Writing data only when an epoch is finished, where an epoch is the interval between the snapshots. During an epoch to snapshot the graph, the operator doesn't write any data. Applicable only for the Python Operator \(`'api.set_epoch_complete_callback'`\) and Kafka Consumer.

> ### Note:  
> Failure happens when the epoch completes, but before persisting data. The data recovery is from the completed epoch, so the writer requires a WAL to determine that the epoch hasn't saved the state yet.



</td>
</tr>
<tr>
<td valign="top">

**Can discard duplicates**

</td>
<td valign="top">

The operator has to guarantee by an independent log that it discards repeated batches before they're propagated to the graph. Discarding repeated batches before propagating to the graph is guaranteed by several operators in the graph. An operator that is directly connected to the generators can have the independent log. Alternately, the source operator can have the independent log.

The **Discard duplicate messages after source** condition is necessary for operators whose internal states are affected by duplicate input messages. Otherwise, there's no risk of having the operators process the data again, and the idempotent writers is enough to prevent external side effects.

</td>
</tr>
</table>



### Other Conditions

**Pipeline is deterministic**

The graph always produces the same data to write and the same internal state for a given set of messages provided by the generators.

Recovering a graph with replayable sources has the same effect as the original run. The generators create the same data of the latest persisted snapshot, which in turn produces the same effects.



### Guarantees

The following table describes the values that appear in the Guarantees column.


<table>
<tr>
<td valign="top">

**Exactly once**

</td>
<td valign="top">

Execution is equivalent to failure-free execution.

</td>
</tr>
<tr>
<td valign="top">

**At most once**

</td>
<td valign="top">

If there's a failure, data is lost but not duplicated.

</td>
</tr>
<tr>
<td valign="top">

**At least once**

</td>
<td valign="top">

If there's a failure, data isn't lost and is duplicated.

</td>
</tr>
</table>

> ### Note:  
> The guarantees are for cases with a single generator or writer, such as a graph that contains the following construction: *Read File* \> *Python Operator* \> *Write HANA.* The listed guarantees are also applicable to any other configuration, excluding cycles.

