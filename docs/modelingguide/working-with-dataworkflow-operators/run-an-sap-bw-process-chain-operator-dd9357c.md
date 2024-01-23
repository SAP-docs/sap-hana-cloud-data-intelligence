<!-- loiodd9357c7f5e34a3ea9a0607f0b8f2e56 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Run an SAP BW Process Chain Operator

To run \(execute\) an SAP Business Warehouse \(BW\) process chain in an SAP BW system, use the BW Process Chain operator in the SAP Data Intelligence Modeler application.



<a name="loiodd9357c7f5e34a3ea9a0607f0b8f2e56__prereq_fd5_t1w_tdb"/>

## Prerequisites

Create a connection to an SAP BW system using the SAP Data Intelligence Connection Management application.



## Context

The SAP BW Process Chain operator contains a sequence of processes that are scheduled to wait in the background for an event. Some of these processes can trigger a separate event that can, in turn, start other processes.

In the SAP BW Process Chain operator, define the start condition of a process chain with the start process type. All other processes in the chain are scheduled to wait for an event. These processes are connected using events that are triggered by an upstream process to start a downstream process.



## Procedure

1.  Log into SAP Data Intelligence and select the Modeler tile.

2.  Open the *Graphs* tab in the navigation pane at left.

3.  Select :heavy_plus_sign: from the navigation pane toolbar, and select *Use Generation 1 Operators*.

    The Modeler opens an empty graph editor at right, and opens the *Operators* tab in the navigation pane.

4.  Select the operator by performing the following substeps:

    1.  Enter “BW Process Chain” in the search bar.

    2.  In the search results, double-click the *BW Process Chain* operator.

        The Modeler adds the *BW Process Chain* operator to the graph editor workspace.


5.  Configure the *BW Process Chain* operator by performing the following substeps:

    1.  Select the *BW Process Chain* operator in the graph editor, and choose <span class="SAP-icons"></span> \(Show Configuration\). 

    2.  Select :pencil2: in the *SAP BW Connection* option.

    3.  Enter a connection ID in *Connection ID* that references a connection to a remote SAP BW system, and choose *Save*.

        To manually enter the connection details to the remote system, select *Manual* in the *Configuration Type* list and enter the required connection details in *Connection ID*.

    4.  Select an SAP BW process chain from the *SAP BW ProcessChain ID* list to run it in the remote system.

        The Modeler populates the list based on the connection ID.

        > ### Restriction:  
        > When the *Configuration Type* for the *SAP BW Connection* is *Manual*, you must enter the *SAP BW ProcessChain ID* manually.

    5.  **Optional:** Enter the request timeout in seconds in *Request Timeout \(seconds\)*.

        The engine waits the set number of seconds for receiving a response from the BW system. The default value is 480 seconds.

    6.  **Optional:** Enter the time interval in seconds in *Retry Interval*.

        The engine waits the set number of seconds until checking the status update of the BW Process Chain. The default value is 20 seconds.

    7.  **Optional:** Enter the maximum number of attempts in *Retry Attempts*.

        The engine queries the status update for the set number of attempts. The default value is 1080 attempts.


    > ### Note:  
    > The Modeler uses only the value of *Retry Interval* if the BW system sends a successful response \(status code 200\) when the Modeler checks the status of the executed BW Process Chain.
    > 
    > For long-running Process Chains, in cases when the Process Chain doesn't complete or fails, the maximum time limit for polling the status is 14 days.
    > 
    > If the Modeler receives a response code other than 200, it uses the value set in *Retry Attempts* along with the setting in *Retry Interval* to check the status of the BW Process Chain.
    > 
    > The operator execution fails and the Modeler sends a message to the error output port under the following circumstances:
    > 
    > -   The engine doesn't receive a response from the BW system within the number of seconds specified in *Request Timeout \(seconds\)*.
    > -   The engine reaches the maximum time limit \(14 days\), which means that the status of the SAP HANA Flowgraph is other than “completed”, “failed” or “canceled”.
    > -   The engine exceeds the number of seconds set in \(*Retry Interval*\) \* \(*Retry Attempts*\), which means that the BW system never returned a response with status code 200 when it checked the status update of the Process Chain.

6.  Save and run the graph.

    You can control the start and stop of the graph execution using the Workflow Trigger and Workflow Terminator operators respectively.

    > ### Tip:  
    > You can also schedule the graph execution. For more information, see [Schedule Graph Executions](../using-graphs/schedule-graph-executions-cb46d5f.md).


**Related Information**  


[Working with the Data Workflow Operators](working-with-the-data-workflow-operators-f3f4333.md "SAP Data Intelligence Modeler has a category of operators called Data Workflow operators. When used in a graph (pipeline) and executed, the Data Workflow operators run for a limited time and finish with the status of either “completed” or “dead”.")

[Create a Connection](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/e259041c90734cb688e13a7931e7d721.html "Create a connection in SAP Data Intelligence, which represents an access point to a remote system or a remote data source.") :arrow_upper_right:

