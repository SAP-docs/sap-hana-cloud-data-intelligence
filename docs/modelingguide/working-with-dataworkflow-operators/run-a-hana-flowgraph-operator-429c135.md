<!-- loio429c135ef23842b5a6d303914b8febae -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Run a HANA Flowgraph Operator

To run \(execute\) an SAP HANA Flowgraph in an SAP HANA system, use the HANA flowgraph operator in the SAP Data Intelligence Modeler application.



<a name="loio429c135ef23842b5a6d303914b8febae__prereq_vcd_1lv_tdb"/>

## Prerequisites

Before you perform the following process, ensure that you first create a connection to an SAP HANA system using the SAP Data Intelligence Connection Management application.



## Context

Executing a HANA Flowgraph operator in a graph helps you transform data from a remote source into SAP HANA either in batch or real-time mode. The flowgraphs are predefined in the server and represent a complete data flow. Select the required SAP HANA flowgraph, and all the operations that the flowgraph must perform are defined in the server.

> ### Note:  
> The Modeler supports executing only XSC-based HANA flowgraphs.



## Procedure

1.  Log into SAP Data Intelligence and select the Modeler tile.

2.  Open the *Graphs* tab from the navigation pane at left.

3.  Select :heavy_plus_sign: from the navigation pane toolbar, and select *Use Generation 1 Operators*.

    The Modeler opens an empty graph editor at right, and opens the *Operators* tab in the navigation pane.

4.  Select the operator by performing the following substeps:

    1.  Enter “HANA Flowgraph” in the search bar.

    2.  Double-click the *HANA Flowgraph* operator in the search results.

        The Modeler adds the *HANA Flowgraph* operator to the graph editor workspace.


5.  Double-click the *HANA Flowgraph* operator in the graph editor.

6.  Complete the *Operator Details* group of options by performing the following substeps:

    1.  Enter the required connection ID in *Connection*.

        Alternately, browse and select the required connection.

    2.  Browse and select the required SAP HANA flowgraph in *SAP HANA Flowgraph*.

    3.  **Optional:** Enter a time interval in seconds in *Retry Interval*.

        The *Retry Interval* specifies the time in seconds for the engine to wait until the next status update. The default value is 20 seconds.

    4.  **Optional:** Enter a value in *Retry Attempts*.

        The *Retry Attempts* specifies the number of attempts to query for the status update. The default value is 10 attempts.


    > ### Note:  
    > If the BW system sends a successful response \(status code 200\) when the Modeler checks the status of the executed BW Process Chain, the Modeler uses only the value of *Retry Interval*. For long-running Process Chains that don't complete or they fail, the maximum time limit for polling the status is 14 days. If the Modeler receives a response code other than 200, it uses the value of *Retry Attempts* with *Retry Interval* to check the status of the BW Process Chain.
    > 
    > The operator execution fails and the Modeler sends a message to the error output port under the following circumstances:
    > 
    > -   A response from the BW system isn't received within the number of seconds specified in *Request Timeout \(seconds\)*.
    > -   The maximum time limit \(14 days\) is reached, which means that the status of the SAP HANA Flowgraph is other than “completed”, “failed” or “canceled”.
    > -   The number of seconds set in \(*Retry Interval*\) \* \(*Retry Attempts*\) is exceeded, which means that the BW system never returned a response with status code 200 when it checked the status update of the Process Chain.

7.  **Optional:** Update the *Variables* section by performing the following substeps:

    In the *Variable* section, the Modeler displays the variables associated with the SAP HANA flowgraph, its data type, and default value. You can edit the default value of a variable.

    1.  Select :pencil2: in the *Variables* section.

    2.  Enter new variable values as applicable.


8.  **Optional:** Update the *Table Variables* section by performing the following substeps:

    In the *Table Variables* section, the Modeler displays the table variables associated with the SAP HANA flowgraph, its data type, and default value. You can edit the default value of a table variable or define new table variables.

    1.  Enter \(or select\) the name of the table variable in the *Table Variables* section under the *Name* column.

    2.  Select :pencil2: in the *Value* text field and provide the required variable value.

    3.  Select :heavy_plus_sign: to define a new table variable for the selected SAP HANA flowgraph.


9.  Save and run the graph.

    You can control the start and stop of the graph execution using the Workflow Trigger and Workflow Terminator operators respectively.

    > ### Tip:  
    > You can also schedule the graph execution. For more information, see [Schedule Graph Executions](../using-graphs/schedule-graph-executions-cb46d5f.md).


**Related Information**  


[Working with the Data Workflow Operators](working-with-the-data-workflow-operators-f3f4333.md "SAP Data Intelligence Modeler has a category of operators called Data Workflow operators. When used in a graph (pipeline) and executed, the Data Workflow operators run for a limited time and finish with the status of either “completed” or “dead”.")

[Create a Connection](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/e259041c90734cb688e13a7931e7d721.html "Create a connection in SAP Data Intelligence, which represents an access point to a remote system or a remote data source.") :arrow_upper_right:

