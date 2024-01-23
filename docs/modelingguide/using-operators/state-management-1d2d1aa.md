<!-- loio1d2d1aae1b40425789d3e70d518f7ab0 -->

# State Management

Use the state management feature by implementing a series of functions in the Python3 operator.

Use the functions in the following table to support recovery and to store states. SAP Data Intelligence doesn't require that you implement all of the functions to store states.


<table>
<tr>
<th valign="top">

Function

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`api.set_initial_snapshot_info(initial_process_info: api.InitProcessInfo)`

</td>
<td valign="top">

Sets the initial information for state management before the operator starts. You can call the initial information outside callback functions.

The parameter `initial_process_info` has two attributes:

-   `is_stateful`: Boolean that specifies that the operator persists states.
-   `outports_info`: Map of port names to `api.OutportInfo`.

    `api.OutportInfo` is a class of one attribute: `is_generator`. The parameter `outports_info` indicates whether output ports of the script operator are generators.




</td>
</tr>
<tr>
<td valign="top">

`api.set_restore_callback(callback)`

</td>
<td valign="top">

Register function that restores the operator state.

**Arguments:** `callback (func[str, bytes] -> None])`.

The function expects the following input parameters:

-   Epoch, which uniquely identifies the state that is being recovered.
-   Serialized operator state.



</td>
</tr>
<tr>
<td valign="top">

`api.set_serialize_callback`

</td>
<td valign="top">

Register function that returns the operator state.

**Arguments:** `callback (func[str] -> bytes)`.

The function expects the epoch as a parameter. Epoch uniquely identifies the state that is being recovered. It returns the serialized operator state.

</td>
</tr>
</table>

Operators with support to state management can have two extra classes: generator and writer.

**Generator**

A generator is a port that produces outputs independent of input port data. All graphs that have data flowing have at least one generator output port. Examples of generators include the following:

-   operators reading files with no input connected
-   Kafka consumers

**Writers**

A writer is an operator that has effects outside the graph \(for example, operators writing into databases, or operators writing to a publisher or subscriber queue\). If an operator is a writer and it's stateful, it offers an “at-least-once” guarantee. An “at-least-once” guarantee means that there's a guarantee that no data is lost, even though it can be written twice. Being stateful requires implementing the restore and serialize functions. It's also possible to have an exactly once guarantee, which requires the writer to be idempotent and stateful. Idempotency means equivalency when writing the same data several times.

Keep in mind the following information regarding state management:

-   To avoid deadlocks, don't block a port callback while it waits for another port callback.
-   Before saving a state, the Modeler doesn't pause the shutdown function. Therefore, the shutdown function doesn't change the operator state.
-   If the operator has asynchronous behavior, the operator must support pause and resume.

For more information about these functions, see the Python3 Operator V2 section of the *Repository Objects Reference* guide.



## Example

> ### Sample Code:  
> ```
> counter = 0
> 
> def on_input(msg_id, header, body):
>     global counter
>     counter += 1
>     api.outputs.output.publish(str(counter))
> 
> api.set_port_callback("input", on_input)
> 
> api.set_initial_snapshot_info(api.InitialProcessInfo(is_stateful=True))
> 
> def serialize(epoch):
>     return pickle.dumps(counter)
> 
> api.set_serialize_callback(serialize)
> 
> def restore(epoch, state_bytes):
>     global counter
>     counter = pickle.loads(state_bytes)
> 
> api.set_restore_callback(restore)
> 
> def complete_callback(epoch):
>     api.logger.info(f"epoch {epoch} is completed!!!")
> 
> api.set_epoch_complete_callback(complete_callback)
> ```

-   **[Examples: Operator States](examples-operator-states-a2269e1.md "This section contains examples illustrating the use of state management functions in the Python3 operator for graph snapshots and operator
        states for Gen2 graphs.")**  
This section contains examples illustrating the use of state management functions in the Python3 operator for graph snapshots and operator states for Gen2 graphs.

**Related Information**  


[Error Recovery with Generation 2 \(Gen2\) Pipelines](../using-graphs/error-recovery-with-generation-2-gen2-pipelines-1cd3efb.md "Gen2 pipelines (graphs) make it possible to recover from errors using specific runtime features.")

