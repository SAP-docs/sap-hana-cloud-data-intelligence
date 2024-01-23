<!-- loio439d0a03a73144e59fc2e35e0bf8e450 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Running Graphs

After creating a graph, you can run the graph based on the configuration defined for the graph. The Modeler application runs the operators in the graph as individual processes.



## Procedure

1.  Open the applicable graph in a graph editor.

2.  Select the down arrow next to :arrow_forward: in the editor toolbar.

3.  Choose one of the run choices.

    -   *Run*: Runs the graph immediately.
    -   *Run As*: *Run As*: Runs the graph after you configure additional settings, such as automatic restart, and snapshots. The following table describes the *Run As* options.

    > ### Note:  
    > The *Run* and *Run As* options trigger graph validation before running the graph. The Modeler displays the results in the *Validation* tab. For more information, see [Validate Graphs](validate-graphs-0857b43.md).

4.  Complete the options in the *Run As* dialog box as described in the following table.


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
    
    *Run Graph As*
    
    </td>
    <td valign="top">
    
    Required. Specifies a unique name for the run.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Trace Level*
    
    </td>
    <td valign="top">
    
    Sets the trace severity threshold, which determines the trace messages that are sent to the trace server. Choose one of the following options:

    -   INFO
    -   DEBUG
    -   ERROR
    -   FATAL
    -   WARN

    For complete descriptions of the Trace Level options, see [Trace Severity Levels](trace-severity-levels-34cad34.md).
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Configuration Substitutions group*
    
    </td>
    <td valign="top">
    
    Contains all the configuration substitution parameters for the operators in the graph.

    If you defined configuration substitution parameters for the operators in the graph, all the configuration substitution parameters display in the *Configuration Substitutions* group.

    Provide the required values for the following options as necessary:

    -   HANA\_DB
    -   file\_connection\_id
    -   file\_path
    -   select\_statement

    > ### Note:  
    > If there are conditional configuration properties for an operator, regardless of the property that is visible in the configuration panel, the *Run As* dialog box still displays all the configuration substitution parameters. It's optional to provide values for the substitution parameters that are hidden in the Modeler.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Capture Snapshot*
    
    </td>
    <td valign="top">
    
    Saves a snapshot \(intermediate state\) of the graph for efficient recovery.

    > ### Note:  
    > Snapshot configuration is available for graphs only with Generation 2 operators.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Every x second\(s\)*
    
    </td>
    <td valign="top">
    
    Specifies the time frequency \(in seconds\) for the *Capture Snapshot* option. Frequence is from 1 second to 24 hours.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Automatic Recovery*
    
    </td>
    <td valign="top">
    
    Restarts the graph automatically if there are failures or system upgrades.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Retry Count*
    
    </td>
    <td valign="top">
    
    Sets the number of retries for recovery within a specific time period.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Retry Interval*
    
    </td>
    <td valign="top">
    
    Sets the interval in seconds between retries for recovery.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Retry Threshold Value*
    
    </td>
    <td valign="top">
    
    Sets the amount of time the system tries to recover the graph before it resets the automatic recovery count.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Remember Configuration Parameters*
    
    </td>
    <td valign="top">
    
    Saves the *Run As* values to the configuration substitution parameters for when you run the graph again. If you’ve saved the configuration for the next graph execution, you can select the configuration for running the graph or update the existing run configuration.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Set as Default Run Configuration*
    
    </td>
    <td valign="top">
    
    Saves the current settings as the default setting. Applicable when you've defined and saved multiple configurations.
    
    </td>
    </tr>
    </table>
    
5.  Select *OK* to save your settings and to start running the graph.


-   **[Automatic Graph Recovery](automatic-graph-recovery-4bf172b.md "Configure any graph to recover from failure automatically, regardless of whether the graph uses Generation 1 or Generation 2 operators. ")**  
Configure any graph to recover from failure automatically, regardless of whether the graph uses Generation 1 or Generation 2 operators.
-   **[Parameterize the Graph Run Process](parameterize-the-graph-run-process-f3caf16.md "Parameterize the graph run process using parameters that assume different values based on the values passed in each graph run.
			")**  
Parameterize the graph run process using parameters that assume different values based on the values passed in each graph run.
-   **[Debug Graphs](debug-graphs-06b0159.md "You can start the graph in debug mode to verify the input and output from each
		operator during execution and analyze or modify the data passing through a connection. ")**  
You can start the graph in debug mode to verify the input and output from each operator during execution and analyze or modify the data passing through a connection.
-   **[Schedule Graph Executions](schedule-graph-executions-cb46d5f.md "The SAP Data Intelligence
		Modeler provides capabilities to schedule graph executions. ")**  
The SAP Data Intelligence Modeler provides capabilities to schedule graph executions.

**Related Information**  


[Schedule Graph Executions](schedule-graph-executions-cb46d5f.md "The SAP Data Intelligence Modeler provides capabilities to schedule graph executions.")

