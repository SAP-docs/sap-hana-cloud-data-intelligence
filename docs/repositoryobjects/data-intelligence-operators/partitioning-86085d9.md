<!-- loio86085d9ccd9d49f69464e7c8e6c6f91f -->

# Partitioning

Data partitioning separates large datasets into smaller ones based on a set of defined criteria.

These partitions can run sequentially or in parallel. For running in parallel, place the next Flowagent Producer inside a group with multiplicity greater than one. The multiplicity defines the number of partitions loaded concurrently. If the Producer is not inside a group, or when the multiplicity is equal to one, the data is loaded sequentially.

Partitioning breaks down one large operation into multiple new operations. The quantity of new operations is usually unknown. Therefore, it can be difficult to know when to stop a graph, for example, after all the partitions are loaded.

When the number of partitions is known, use a Constant Generator that receives the number of partition messages from the Producer. After all messages are received, the Constant Generator sends a signal to the Graph Terminator, which ends the graph.

A simpler approach, however, is to use the outMessage port of the Producer operator, and add a Message Operator, modifying the script by adding the following Javascript code:

> ### Sample Code:  
> ```
> $.setPortCallback("input", onInput);
> 
> var partitionCount = 0;
> 
> function onInput(ctx, s) {
>     var partitionCountTotal = s.Attributes['producer.partition.count'];
>     if ((s.Attributes['producer.type'] == "CSV" && s.Attributes['message.lastBatch'] === true) || s.Attributes['producer.type'] == "FILE" || s.Attributes['producer.type'] == "TABLE") {
>         partitionCount++;
>     }
>     if (partitionCount == partitionCountTotal) {
>         $.output(s);
>     }
> }
> ```

The Message Operator waits for all partitions to finish processing. Then it sends a message to the next operator. If the next operator is a Graph Terminator, the graph processing is finished.

-   **[Logical Partitions](logical-partitions-83ccb1c.md "Logical partitions are user-defined chunks of data, where each chunk contains a filter that specifies the chunk of data to be
		read.")**  
Logical partitions are user-defined chunks of data, where each chunk contains a filter that specifies the chunk of data to be read.
-   **[Graph Termination Using Partition](graph-termination-using-partition-76478fd.md "Learn how to stop a graph with partitions based on the operator generation.")**  
Learn how to stop a graph with partitions based on the operator generation.
-   **[Partitioned Files](partitioned-files-34eab43.md "Partitioned files represent separated chunks of a single file.")**  
Partitioned files represent separated chunks of a single file.

