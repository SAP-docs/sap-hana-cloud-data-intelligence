<!-- loio3fe55dded73847f09d783a22b20aec21 -->

# Example Notification

This graph serves as an example on how to use SAP Data Intelligence and Pipeline operators from the Data Workflows category.



In the graph, the Pipeline operator starts an internal example graph \(`com.sap.demo.counter`\) as a subgraph. If the example graph terminates with the status “dead”, an email notification will be sent to the configured email addresses.



<a name="loio3fe55dded73847f09d783a22b20aec21__section_olg_zlk_dfb"/>

## Configure and Run the Graph

Follow the steps below to run the graph from SAP Data Intelligence Modeler:

1.  In the left panel, select the *Graphs* tab and open the *Example Notification*graph.
2.  In the tool bar, select *Run* \(play button\).
3.  The *Status* panel indicates if the graph is running.
4.  The example graph will appear in the *Status* panel and the status is "running".

To show the status of the example graph, toggle on *Show Subgraphs.*



<a name="loio3fe55dded73847f09d783a22b20aec21__section_vpb_mmk_dfb"/>

## Configuring the Pipeline Operator \(Optional\)

By default, the example graph is configured to terminate itself. In this context, the Data Workflow waits for the example graph to finish and will turn into “completed” after the example graph finishes. If you want to run another graph without waiting for the graph to finish, follow the steps below:

1.  Select *Pipeline* operator and open the configuration.
2.  Go to *Graph Name*and select a graph from the list.
3.  Go to *Running Permanently* and choose *true* from the list.

If you want to run a graph on a remote system, follow the documentation of [Pipeline](../data-intelligence-operators/pipeline-4525f87.md).



<a name="loio3fe55dded73847f09d783a22b20aec21__section_sfx_knk_dfb"/>

## Configuring the Notification Operator

1.  Select *Notification* operator and open the configuration.
2.  Go to *Connection*, choose either *Configuration Manager* or *Manual*. When using *Configuration Manager*, create a connection via *Connection Management*first.

    > ### Note:  
    > It is recommended to choose *Configuration Manager* as the configuration type and select an existing *Connection ID*. The *Manual* configuration type must be used only for testing purposes.

3.  Go to *Default From Value* and input an email address as sender.
4.  Go to *Default To Value* and input one or more receiver email addresses.
5.  Go to *Default Subject Value* to give a subject to the email.

