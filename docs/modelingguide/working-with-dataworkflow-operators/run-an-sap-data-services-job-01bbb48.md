<!-- loio01bbb484ba2a41a5984560b6d72fcff1 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Run an SAP Data Services Job

Use the SAP Data Services Job operator in the SAP Data Intelligence Modeler application to run \(execute\) an SAP Data Services job in a remote system.



<a name="loio01bbb484ba2a41a5984560b6d72fcff1__prereq_fd5_t1w_tdb"/>

## Prerequisites

Create a connection to an SAP Data Services system using the SAP Data Intelligence Connection Management application.



## Context

Running an SAP Data Services job helps you integrate, transform, and improve the data quality. In SAP Data Services, the unit of execution is called a job. Running an SAP Data Services job in SAP Data Intelligence helps you in the following ways:

-   Ingesting data into a Hadoop cluster for further processing \(natively in a Hadoop cluster\).
-   Moving data out of SAP Data Intelligence after processing.



## Procedure

1.  Log into SAP Data Intelligence and select the *Modeler* tile.

2.  Open the *Graphs* tab in the navigation pane at left.

3.  Select :heavy_plus_sign: from the navigation pane toolbar, and select *Use Generation 1 Operators*.

    The Modeler opens the graph editor in the workspace and opens the *Operators* tab in the navigation pane automatically.

4.  Select the SAP Data Services Job operator by performing the following substeps:

    1.  Enter “SAP Data Services” in the search bar.

    2.  Double-click the SAP Data Services Job operator under the Remote DataFlow group in the search results.

        The Modeler adds the Pipeline operator to the graph editor workspace.


5.  Configure the operator by performing the following substeps:

    1.  Select <span class="SAP-icons"></span> \(Open Configuration\) to the right of the SAP Data Services Job operator in the workspace.

    2.  Select :pencil2: in the *SAP Data Services Connection* box in the *Configuration* pane.

    3.  Browse for and choose a connection in *Connection ID*.

    4.  Enter a description for the operator in *Description*.

    5.  Browse for and select the required SAP Data Services job in *Job*.

        The Modeler populates the *Repository* field automatically with the repository that contains the SAP Data Services job. The Modeler also displays the global variables and the substitution parameters \(if any\) that are associated with the job in the Global Variables table.

    6.  Choose the required Job Server from the *Job Server* list.

        The Modeler uses the selected Job Server to run the job.

        > ### Note:  
        > You can also use a Job Server group to run the job. If you select a Job Server group, specify the distribution level \(job level, data flow level, or sub data flow level\).

    7.  Choose the required system configuration details from the *System Configuration* list.

        The Modeler uses the system configuration for running the job.


6.  **Optional:** Edit global variables by performing the following substeps:

    If the selected job is associated with global variables, in the *Global Variables* section the Modeler displays the global variables, its data type, and default value. You can edit the default value of a global variable associated with the job.

    1.  Select :pencil2: in the *Global Variables* box.

        The Modeler populates values in the *Global Variables* section depending on the version of the SAP Data Services system in which you've created the selected job.

    2.  Choose the applicable global variable and select :pencil2: in the *Value* text field and provide the required value.

    3.  To define a new global variable for the SAP Data Services job, in the *Global Variables* section, choose :heavy_plus_sign: and provide the variable and value.

        > ### Note:  
        > Adding new global variables isn't applicable for all Data Services jobs. It depends on the version of the SAP Data Services system in which you've created the selected job.


7.  **Optional:** Edit substitution parameters in the same manner as global variables.

    In the *Substitution Parameters* section, define the substitution parameters associated with the job, its data type, and default value. You can edit the default value of a substitution parameter or define new substitution parameters.

    > ### Note:  
    > Substitution parameters that the application displays in the dropdown list are the parameters that are associated with the selected system configuration.

    > ### Note:  
    > The Modeler doesn't always auto-populate the global variables or substitution parameters. It depends on the version of the SAP Data Services system in which you've created the selected job. If the global variables aren't auto-populated, enter the information manually.

8.  Save and run the graph.

    You can control the start and stop of the graph execution using the Workflow Trigger and Workflow Terminator operators respectively.

    > ### Tip:  
    > You can also schedule the graph execution. For more information, see [Schedule Graph Executions](../using-graphs/schedule-graph-executions-cb46d5f.md).


**Related Information**  


[Working with the Data Workflow Operators](working-with-the-data-workflow-operators-f3f4333.md "SAP Data Intelligence Modeler has a category of operators called Data Workflow operators. When used in a graph (pipeline) and executed, the Data Workflow operators run for a limited time and finish with the status of either “completed” or “dead”.")

[Create a Connection](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/e259041c90734cb688e13a7931e7d721.html "Create a connection in SAP Data Intelligence, which represents an access point to a remote system or a remote data source.") :arrow_upper_right:

