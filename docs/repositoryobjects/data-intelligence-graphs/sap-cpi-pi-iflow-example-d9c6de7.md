<!-- loiod9c6de7253fe4a15afddce12eb4c7745 -->

# SAP CPI-PI iFlow Example

This is a very basic example graph demonstrating how the SAP CPI-PI iFlow operator interacts with connected operators.



## Prerequisites

-   A running SAP CPI instance with at least one deployed iFlow that can be triggered via HTTP.




<a name="loiod9c6de7253fe4a15afddce12eb4c7745__section_itp_js5_bgb"/>

## Configure and Run the Graph

Follow the steps below to run the example:

1.  In the left panel select the *Graphs* tab, navigate to *SAP Integration* and click on *SAP CPI-PI iFlow* to open the graph.
2.  Optional: To not modify the original example, click on the arrow beside the save button and select *Save As*. Save a copy of this graph at a destination of your choice.
3.  Before you can run the graph you need to configure it. Click on the *SAP CPI-PI iFlow* operator, in the *Operator* tab, and enter your connection details \(you may also create a connection in the connection manager app first and then use this one in here\) and the path of your deployed iFlow. Also check whether the set iFlow has an enabled CSRF protection and set the configuration parameter on the operator accordingly.
4.  Now click on the *Constant Generator*operator and enter the payload for the *SAP CPI-PI iFlow* operator in the *Content* field.
5.  In the tool bar, select *Run* \(play button\).
6.  The *Status* panel indicates if the graph is running.
7.  Use the context menu *Open UI* of the *Terminal* operator to open the terminal.
8.  The terminal opens and you should see the data returned from the triggered iFlow.

