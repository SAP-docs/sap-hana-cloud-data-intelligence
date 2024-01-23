<!-- loio76478fd5bd5a4b709e4b28ad23e71224 -->

# Graph Termination Using Partition

Learn how to stop a graph with partitions based on the operator generation.

Data partitioning separates large datasets into smaller ones based on a set of defined criteria. These partitions can run sequentially or in parallel. For running in parallel, place the next Flowagent Producer inside a group with multiplicity greater than one. The multiplicity defines the number of partitions loaded concurrently. If the Producer is not inside a group, or when the multiplicity is equal to one, the data is loaded sequentially.

Partitioning breaks down one large operation into multiple new operations. The quantity of new operations is unknown. Therefore, it can be difficult to know when to stop a graph, for example, after all the partitions are loaded.

The next sections describe how to stop the graph based on the operator generation.



<a name="loio76478fd5bd5a4b709e4b28ad23e71224__section_nb5_lnf_crb"/>

## Generation 1

When the number of partitions is known, use a Constant Generator that receives the number of partition messages from the Producer. After all messages are received, the Constant Generator sends a signal to the Graph Terminator, which ends the graph.

However, a simpler approach is to use the *outMessage* port of the Producer operator to add a Message Operator and modifying the script by adding the following Javascript code:

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



<a name="loio76478fd5bd5a4b709e4b28ad23e71224__section_rff_vnf_crb"/>

## Generation 2

The process to stop a graph is similar to the Generation 1 operators. However, you use the Python operator \(com.sap.system.python3Operator.v2\).

After adding the Python Operator to the graph, map the out port of the Producer to the Python operator. The operator has an input port of name input1. Add the following Python code to the script:

> ### Sample Code:  
> ```
> partition_count = 0
> 
> def on_input(msg_id, header, body):
>     global partition_count
>     
>     # increment partition finished counter
>     partition_count += 1
>     if partition_count + header["com.sap.headers.partition"][2] == header["com.sap.headers.partition"][1]:
>         api.outputs.output.publish("done")
> 
> api.set_port_callback("input1", on_input)
> ```

The Python operator waits for all partitions to finish processing. Then it sends a message to the next operator. If the next operator is a Graph Terminator, the graph processing is finished.

