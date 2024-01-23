<!-- loio2714f1ed833f405c84c0235051ac4f3d -->

# Data Workflow

This graph starts an internal example graph \(com.sap.demo.counter\). It serves as an example on how to use the operators from the Data Workflow category.



## Configure and Run the Graph

Follow the steps below to run the graph from SAP Data Intelligence Modeler:

1.  In the left panel, select the *Graphs* tab and navigate to *Examples* \> *Data Workflow*.
2.  In the tool bar, select *Run* \(play button\).
3.  The *Status* panel indicates if the graph is running.
4.  The example graph will appear in the *Status* panel and the status is "running".



### Configuration \(Optional\)

By default, the example graph is configured to terminate itself. In this context, the Data Workflow waits for the example graph to finish and will turn into "completed" after the example graph finishes. If you want to run another graph without waiting for the graph to finish, follow the steps below:

1.  Open the Data Workflow, select *Pipeline* operator and open the configuration \(the 3rd button\).
2.  Go to *Graph Name* and select a graph from the list.
3.  Go to *Running Permanently* and choose *true* from the list.

If you want to run a graph on a remote system, follow the documentation of [Pipeline](../data-intelligence-operators/pipeline-4525f87.md).

