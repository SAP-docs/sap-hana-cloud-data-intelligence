<!-- loio610a01b4409e4036a2a2662dd027fc3d -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Monitor the Graph Execution Status

After creating and executing a graph, you can monitor the status of the graph execution in the SAP Data Intelligence application.



## Procedure

1.  Start the SAP Data Intelligence Modeler.

2.  Select the *Status* tab in the bottom pane.

    The *Status* tab provides information on the status of all graphs, including graphs that have completed execution.


    <table>
    <tr>
    <th valign="top">

    Action
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    **Customize the view of status panel**
    
    </td>
    <td valign="top">
    
    Display the status of all graphs either in <span class="SAP-icons"></span> \(List View\)where instances of a graph are displayed separately as a list, or in <span class="SAP-icons"></span> \(Tree View\)where instances of a respective graph are grouped into one.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Monitor status of subgraphs**
    
    </td>
    <td valign="top">
    
    When a graph execution triggers the execution of another graph, the other graph is called a subgraph. Monitor the status of various subgraphs that the Modeler has executed by doing the following:

    1.  Open the *Status* tab.
    2.  Enable *Show Subgraphs*.

    You can see subgraphs only in the <span class="SAP-icons"></span> \(List View\).
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Download diagnostic information**
    
    </td>
    <td valign="top">
    
    Download the diagnostic information that the Modeler generates for a graph as a zipped archive.

    1.  In the *Status* tab, next to the required graph, choose <span class="SAP-icons"></span> \(Download Diagnostic Information\).
    2.  Open or save the zipped archive file.

    > ### Note:  
    > If a graph has subgraphs or the graph is a subgraph, the archive contains information about all of the graphs in the hierarchy.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Edit a graph**
    
    </td>
    <td valign="top">
    
    Edit a graph by opening the *Status* tab next to the applicable graph and selecting:pencil2:
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Pause and restart a process**
    
    </td>
    <td valign="top">
    
    Pause the execution of a graph by opening the *Status* tab next to the required graph and selecting <span class="SAP-icons"></span> \(Pause process\).

    Restart the paused graph by selecting <span class="SAP-icons"></span> \(Restart process\). 

    Restarting a graph creates a new instance of the graph with previously saved graph, recovery, and snapshot configurations.

    You can also configure automatic recovery of graph for graph failures. For more information, see [Running Graphs](running-graphs-439d0a0.md).
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Archive instances**
    
    </td>
    <td valign="top">
    
    Archive a single graph instance by selecting <span class="FPA-icons"></span> \(Archive\) next to the applicable graph. You can archive a graph in either <span class="SAP-icons"></span> \(List View\) or <span class="SAP-icons"></span> \(Tree View\).

    To archive multiple graph instances of a group at once, switch to <span class="SAP-icons"></span> \(Tree View\) and select <span class="FPA-icons"></span> \(Archive\) next to the required subgraph.

    > ### Note:  
    > The Modeler archives the graph instances with status *stopped by pause*, *dead*, and *completed*. The Modeler doesn't archive graphs whose latest instance is a valid snapshot with status other than completed.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Archive instances by status**
    
    </td>
    <td valign="top">
    
    Archive graph instances by status by opening the *Status* tab and selecting *Cleanup*. Choose one of the following options:

    -   *Archive only completed instances*
    -   *Archive completed and dead instances*

    To delete any saved snapshots, select the *Delete saved snapshots* checkbox.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **View execution details**
    
    </td>
    <td valign="top">
    
    View additional details about a graph's execution after execution completes.

    **Snapshots enabled:** In the *Status* tab, the symbol <span class="SAP-icons"></span> next to the graph name indicates that the snapshots feature is enabled.

    **Detailed graph information:** To view detailed information about a graph, select the graph name in the *Status* tab. The Modeler opens the graph in the graph editor area and displays a series of tabs below the graph. For example, view information in the following tabs:

    -   *Group* tab: View more information about the groups in a partitioned graph.

        > ### Note:  
        > If you’ve defined a multiplicity of a number greater than 1 for a group, such as 3, the Modeler displays three instances for the same group.

    -   *Process* tab: View details of various processes executed in the graph.
    -   *Metrics* tab: View metrics that the Modeler provides as part of the process.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Stop execution**
    
    </td>
    <td valign="top">
    
    Stop the execution of any graph by opening the *Status* tab, selecting the applicable graph, and choosing <span class="SAP-icons"></span> \(Stop Process\).

    The status of the graph changes to *completed* or *dead* depending on the state of the graph when the execution is stopped.
    
    </td>
    </tr>
    </table>
    

-   **[Graph Execution](graph-execution-e047f2d.md "The Modeler application supports executing a graph and monitoring its status from within
		the application.")**  
The Modeler application supports executing a graph and monitoring its status from within the application.
-   **[Graph Status](graph-status-090bce6.md "When you create a graph, each graph is associated with a graph status, which may vary with time and can be manipulated with operations on
		the graph.")**  
When you create a graph, each graph is associated with a graph status, which may vary with time and can be manipulated with operations on the graph.
-   **[Process Status](process-status-2930d4a.md "When you execute a graph, the tool executes each operator in the graph as processes. Each process execution is associated with a status,
		which may vary with time.")**  
When you execute a graph, the tool executes each operator in the graph as processes. Each process execution is associated with a status, which may vary with time.
-   **[Graph Execution Garbage Collection](graph-execution-garbage-collection-2bd7610.md "To maintain the cluster, the Modeler employs Graph Garbage Collection using the following strategies: time-based and
		number-based.")**  
To maintain the cluster, the Modeler employs Graph Garbage Collection using the following strategies: time-based and number-based.

