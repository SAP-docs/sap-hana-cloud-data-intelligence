<!-- loio1cd3efbc60a2442085e71afc733b73a1 -->

# Error Recovery with Generation 2 \(Gen2\) Pipelines

Gen2 pipelines \(graphs\) make it possible to recover from errors using specific runtime features.

Configure the following features at runtime for your Gen2 graphs to aid in pipeline recovery when errors occur:

-   **Auto Restart:** Graphs restart automatically when the pipeline fails or is evicted.
-   **Snapshots:** Graphs create periodic snapshots of the current operation. Benefits of snapshots include the following:
    -   Recover the operation when there are failures, pauses, or system upgrades.
    -   Save information about individual tasks, such as row last read, so that you can view task information when you recover the pipeline.
    -   Restart a pipeline at the point of error. Script operators implement an API for saving and restoring the state, which allows you to implement more complex use cases.

        > ### Note:  
        > For more information about snapshots and limitations, see [Graph Snapshots and Operator States](graph-snapshots-and-operator-states-f206c72.md).


-   **Streaming API:** Use streaming API during data transfor. Loads small chunks of data into system memory instead of data from the entire pipeline. Streaming API has the following benefits:
    -   Reduce overall memory usage: Operators send and consume data in small chunks inside the same stream, which reduces memory usage.
    -   Combine with batch: Operators send each batch as a stream, and include the metadata for each batch inside the headers.


> ### Tip:  
> When you implement runtime features for Gen2 graphs, use standardized error handling so that each operator uses the same methods for processing errors.

To design and operate recoverable Gen2 graphs, use the following methods:

-   Gen2 Runtime:


    <table>
    <tr>
    <th valign="top">

    Option
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Auto Restart
    
    </td>
    <td valign="top">
    
    Configure graphs to restart automatically on failure or eviction. Set the *Automatic Recovery* options in the *Run As* dialog box.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Snapshots
    
    </td>
    <td valign="top">
    
    Configure graphs to save a snapshot of the current operation periodically. The snapshot allows recovery of the operation when the graph fails, pauses, or when there are system upgrades. Operators save information about individual tasks, such as which row in a table was last updated, and receive that information on recovery, avoiding the need to restart the whole operation from the beginning. There are also functions for script operators that implement an API for saving and restoring state as well, allowing users to implement more complex use cases.
    
    </td>
    </tr>
    </table>
    
-   Streaming: Operators support a streaming API for data transfer that doesn't require loading all information into memory. Operators can send and consume data in small chunks inside the same stream, reducing overall memory usage. Sending data through batches is still possible but it can be combined with streams. Operators can send each batch as a stream with the metadata for each batch being sent inside the headers.
-   Error Handling: Each operator has a standardized way of handling errors.

**Related Information**  


[Graph Snapshots and Operator States](graph-snapshots-and-operator-states-f206c72.md "You can configure Generation 2 (Gen2) graphs to take snapshots of their state at regular time intervals so that the operators of the graph send small pieces of data (status) to a central data store.")

[State Management](../using-operators/state-management-1d2d1aa.md "Use the state management feature by implementing a series of functions in the Python3 operator.")

