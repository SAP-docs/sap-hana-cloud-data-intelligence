<!-- loio69bbcf990caa4439b24515dd02b42918 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Run an SAP Data Intelligence Pipeline

Use the Pipeline operator in the SAP Data Intelligence Modeler application to run \(execute\) a graph \(pipeline\) in an SAP Data Intelligence system.



## Context

Use the Pipeline operator to run a graph in a remote SAP Data Intelligence system or in a local system. A graph represents a concrete and complex data flow and helps transform data between elements connected in a series. When you run a graph, it can help process the raw data from multiple sources and make the data available for different use cases.



## Procedure

1.  Log into SAP Data Intelligence and select the Modeler tile.

2.  Open the *Graphs* tab in the navigation pane at left.

3.  Select :heavy_plus_sign: from the navigation pane toolbar, and select *Use Generation 1 Operators*.

    The Modeler opens the graph editor in the workspace and opens the *Operators* tab automatically.

4.  Enter “Pipeline” in the search bar and double-clidk the Pipeline operator in the search results.

    The Modeler adds the Pipeline operator to the graph editor workspace.

5.  Configure the operator by performing the following substeps:

    1.  Select <span class="SAP-icons"></span> \(Open Configuration\) to the right of the Pipeline operator in the workspace.

    2.  Select :pencil2: in the *VFlow Connection* box in the *Configuration* pane.

        The *Edit Property* dialog box opens.

    3.  Enter a connection ID in one of the following ways:

        -   If you've already created connections in the SAP Data Intelligence Connection Management application, select the dropdown arrow at the end of the *Connection ID*option and choose the required connection.
        -   To enter the connection manually, first choose *Manual* from the *Configuration Type* list.

        > ### Note:  
        > Providing connection details for the Pipeline operator is necessary only to run a graph in a remote SAP Data Intelligence system. If you don't provide a value, you can run only a pipeline from the local system. A pipeline from the local system is one that you're working on currently in the SAP Data Intelligence Modeler.

    4.  Select *Save*.

        The *Edit Property* dialog box closes.

    5.  Choose the SAP Data Intelligence graph \(pipeline\) to run from the *Graph Name* list in the *Configuration* pane.

        The Modeler populates the list with all graphs in the remote system, based on the connection ID, or all graphs available in the local system.

    6.  **Optional:** Enter the time interval in seconds in *Retry Interval*.

        The engine waits the set number of seconds until the next status update. The default value is 20 seconds.

    7.  **Optional:** Enter the maximum number of attempts in *Retry Attempts*.

        The engine queries for the status update for the set number of attempts. The default value is 10 attempts.

        > ### Note:  
        > If the Pipeline operator exceeds the settings for both *Retry Interval* and *Retry Attempts*, the graph run fails and the Pipeline operator sends a message to the error output port. The Pipeline operator exceeds the settings when it has requested a status update for the set number of times in *Retry Attempts* and the Modeler hasn't executed the graph, or the graph executed with errors.

    8.  Choose a value from the *Running Permanently* list to indicate whether the selected SAP Data Intelligence graph is running permanently.

        The following table describes the values for *Running Permanently*.


        <table>
        <tr>
        <th valign="top">

        Value
        
        </th>
        <th valign="top">

        Description
        
        </th>
        </tr>
        <tr>
        <td valign="top">
        
        *true* 
        
        </td>
        <td valign="top">
        
        The operator execution checks whether the graph is in a running state. If the graph isn't running, the operator starts the graph execution and terminates immediately \(status: completed\), while the graph remains in the running state. But, if the task is already running with a different task version, then the already-running instance is stopped, and the new task version is started and then terminated immediately \(status: completed\).
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        *false* 
        
        </td>
        <td valign="top">
        
        The operator runs the graph once, and the operator execution terminates after the graph execution terminates. *False* is the default value.
        
        </td>
        </tr>
        </table>
        

6.  Save and run the graph.

    You can control the start and stop of the graph execution using the Workflow Trigger and Workflow Terminator operators respectively.

    > ### Tip:  
    > You can also schedule the graph execution. For more information, see [Schedule Graph Executions](../using-graphs/schedule-graph-executions-cb46d5f.md).


**Related Information**  


[Working with the Data Workflow Operators](working-with-the-data-workflow-operators-f3f4333.md "SAP Data Intelligence Modeler has a category of operators called Data Workflow operators. When used in a graph (pipeline) and executed, the Data Workflow operators run for a limited time and finish with the status of either “completed” or “dead”.")

[Create a Connection](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/e259041c90734cb688e13a7931e7d721.html "Create a connection in SAP Data Intelligence, which represents an access point to a remote system or a remote data source.") :arrow_upper_right:

