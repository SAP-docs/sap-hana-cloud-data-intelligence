<!-- loioe352e7f1a99e4b5d989db5ae1e5e5d0b -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Using the Monitoring Application

The SAP Data Intelligence Monitoring application offers the following capabilities.

Tenant administrator users, and developer member users with the sap.dh.monitoring policy can view all tenant users statistics. Member users without the monitoring policy can view information only for their graphs.

> ### Note:  
> Developer member users with the sap.dh.monitoring policy can filter the information based on specific users.


<table>
<tr>
<th valign="top">

Actions

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Visualize various aspects of graph execution in the *Analytics* tab.

</td>
<td valign="top">

The *Analytics* tab is a dashboard that contains various tiles with targeted information about graphs. The following table describes each tile of the *Analytics* tab.


<table>
<tr>
<th valign="top">

Tile

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

*Status*

</td>
<td valign="top">

A pie chart with the following information:

-   The number of graph instances executed in the Modeler.
-   The status of graph instances executed. Each sector in the pie chart represents a graph state.



</td>
</tr>
<tr>
<td valign="top">

*Runtime Analysis*

</td>
<td valign="top">

A scatter chart that includes a time period axis and duration of graph execution \(in seconds\) axis. This chart provides information on each graph execution and plots them in the scatter chart against the time and duration of execution.

Each point in the chart represents a graph instance. Place your cursor on one instance point for more information about that particular graph instance.

Configure the chart to view results for a selected time period. Use the filter in the chart header to select the time period \(hour, day, and week\).

</td>
</tr>
<tr>
<td valign="top">

*Recently Executed*

</td>
<td valign="top">

Displays the top five instances and execution status. To view all the instances, select *Show All*.

</td>
</tr>
<tr>
<td valign="top">

*Memory Usage*

</td>
<td valign="top">

A line chart for the memory consumption of graphs. Use the filter to display by graph, status, and submission time. You can also see the resource usage in the last hour, day, 2 days, or set the custom time range for which to view the resource consumption.

</td>
</tr>
<tr>
<td valign="top">

*CPU Usage*

</td>
<td valign="top">

A line chart for the CPU consumption of graphs. Filter to display by graph, status, user, or submission time. Also see the resource usage in the last hour, day, 2 days, or set the custom time range for which you want to view the resource consumption.

</td>
</tr>
</table>

> ### Note:  
> The tiles in the *Analytics* tab don't include the information on the archived graph instances.



</td>
</tr>
<tr>
<td valign="top">

View execution details of individual graph instances in the *Instances* tab.

</td>
<td valign="top">

Use the *Instances* tab of the SAP Data Intelligence Monitoring application to view execution details of individual graph instances.

> ### Note:  
> If you're a tenant administrator, you can see graph instances of all users. By default, there's a filter that shows only the administrator's graph instances. Modify the filter to view graph instances of select tenant users on which you can perform limited actions.

> ### Note:  
> If you're a developer member user with the sap.dh.monitoring policy, you can see graph instances of all users just like a tenant administrator.

For each graph instance, the Monitoring application provides information, such as the status of the graph execution, the graph execution name, the source of the graph in the repository, and the time of execution.

To open the execution details pane, select a graph instance. The execution details pane displays more execution details that help you monitor the graph execution.

> ### Note:  
> By default, a filter is applied to exclude the subgraphs and the archived instances from the *Instances* list. You can remove the filter by selecting the :x: icon that corresponds to a filter in the *Filters* bar. Alternately, select the <span class="SAP-icons"></span> Filter icon to set or remove filters.



</td>
</tr>
<tr>
<td valign="top">

View subgraph execution details in the *Instances* tab.

</td>
<td valign="top">

When a graph execution triggers or spawns the execution of another graph, the spawned execution is called a subgraph.

You can filter the view of the Monitoring application to view execution details of all subgraph instances.

To view subgraphs, remove the filter *Exclude Subgraphs* by selecting the :x: icon that corresponds to a filter in the *Filters* bar. Or use the <span class="SAP-icons"></span> Filter icon to set or remove filters. The application refreshes the list view and displays all subgraph instances along with all other graph instances.

> ### Note:  
> All subgraph instances are named as *subgraph*.

To open the execution details pane, select a subgraph instance. The subgraph instance pane displays additional execution details.

</td>
</tr>
<tr>
<td valign="top">

View subgraph hierarchy details in the *Instances* tab.

</td>
<td valign="top">

View the parent graph of a selected subgraph, or view the complete hierarchy of graph instances associated with the subgraph.

1.  Open the *Instances* tab.
2.  Select the <span class="SAP-icons"></span> Select an Action icon next to the applicable subgraph instance.
3.  Select *Show Hierarchy*.

    The Hierarchy dialog box opens displaying all graph instances associated with the selected subgraph in hierarchical order.

4.  Select an applicable graph.
5.  Select *View details*.



</td>
</tr>
<tr>
<td valign="top">

Filter graph instances in the *Instances* tab.

</td>
<td valign="top">

Use the filter tool to control the graphs to view:

1.  Open the *Instances* tab.
2.  Select the <span class="SAP-icons"></span> Add Filter icon.
3.  Define the required filter conditions.

    Filter the listed graphs based on attributes, such as the source name, execution status, time of execution and more.

4.  To filter and view graph instances executed on the same day, hour, or week, select *Hour*, *Day*, or *Week* in the menu bar and the view changes to records for that time frame.

If you're a tenant administrator, you can modify the filter to view graph instances of other users.

Developer member users can modify the filter to view graph instances of other users when they are assigned the sap.dh.monitoring policy.

</td>
</tr>
<tr>
<td valign="top">

Open source graph in the *Instances* tab.

</td>
<td valign="top">

For any selected graph instance, launch the source graph in the Modeler application from the Monitoring application.

1.  Open the *Instances* tab.
2.  Select an instance.

    The application opens a graph overview pane at right that displays the source graph of the selected graph instance.

3.  Select *Open Source Graph* in the menu bar of the overview pane.

    The Monitoring application opens the Modeler application in a new browser tab with the source graph of the selected instance opened in the graph editor.

4.  View or edit the graph configuration.



</td>
</tr>
<tr>
<td valign="top">

View graph configurations in the *Instances* tab.

</td>
<td valign="top">

For any selected graph instance, you can view the configurations defined for its source graph.

1.  Open the *Instances* tab.
2.  Select an instance.

    The application opens a graph overview pane at right that displays the source graph of the selected graph instance.

3.  Select the <span class="SAP-icons"></span> Show Configuration icon.

    The application opens the *Configuration* pane at right where you can view read-only graph configuration information.

4.  **Optional:** Right-click an operator in the graph overview pane and choose *Open Configuration*.

    The *Configuration* pane shows read-only operator configuration information.




</td>
</tr>
<tr>
<td valign="top">

Stop a graph instance execution in the *Instances* tab.

</td>
<td valign="top">

Stop the execution of a graph instance when it's the running or pending state.

1.  Open the *Instances* tab.
2.  Select a graph instance that has a running status.

    The graph overview pane opens at right.

3.  Select the <span class="SAP-icons"></span> Stop Execution icon in the menu bar.



</td>
</tr>
<tr>
<td valign="top">

Search graph instances in the *Instances* tab.

</td>
<td valign="top">

To search for any graph instance, use the search bar in the *Instances* tab. Search for any graph instance based on the instance name or its source graph name.

</td>
</tr>
<tr>
<td valign="top">

Archive graph instance in the *Instances* tab.

</td>
<td valign="top">

Archive a completed or dead graph instance from the Pipeline Engine only.

1.  Open the *Instances* tab.
2.  Select the <span class="SAP-icons"></span> Select an Action icon in the *Actions* column of the applicable instance.
3.  Select *Archive*.

> ### Note:  
> The archived instances remain in the system for a default period of 90 days. The tenant administrator can configure the retention time via the System Management application.



</td>
</tr>
<tr>
<td valign="top">

Download diagnostics information and view logs in the *Instances* tab.

</td>
<td valign="top">

Use the Monitoring application to download graph diagnostics information and view logs to help diagnose and solve errors with graphs.

View logs generated for certain operators, such as the data workflow operator, when you execute the graph.

1.  Open the *Instances* tab.
2.  Select the <span class="SAP-icons"></span> Select an Action icon in the *Actions* column of the applicable instance.
3.  Select *Download Diagnostic Info*.

The application downloads a zipped archive of graph information automatically.

For certain operators, such as the data workflow operators, view logs generated for the operator execution. To view these logs:

1.  Open the *Instances* tab.
2.  Select the graph.

    The graph overview pane opens at right.

3.  Select the *Process Logs* tab in the lower pane.

    The *Logs* tab contains a list of logs for the selected graph.

4.  Use the filter lists at the top of the tab to filter for specific groups and processes, or search for the specific log. Scroll through the processes to read the log texts.



</td>
</tr>
<tr>
<td valign="top">

Manage schedules in the *Schedules* tab.

</td>
<td valign="top">

View graphs that are scheduled for execution and create, edit, or delete schedules.

For more information about scheduling graphs for execution, see “Schedule Graph Executions” in the *Modeling Guide*.

A tenant administrator can view their schedules and the schedules of other users in the Monitoring application. If you're a tenant administrator, you can perform the following tasks in the *Schedules* tab on other users' schedules:

-   View schedules by applying filters.
-   Edit or stop schedules.
-   Suspend or resume schedules.
-   View executed instances of schedules.



</td>
</tr>
<tr>
<td valign="top">

Monitor the execution of replication flows in the *Replications* tab.

</td>
<td valign="top">

View information about replication data flows, including connection details, load progress, and user information.

For tasks, the *Replications* tab displays information, such as the number of tasks in different states, priority settings, number of operations and partitions, and execution timestamps. \(The number of operations displayed may be higher than the actual amount of records transferred as data may be transferred twice in case of error situations.\) Use the *Search* box in the menu bar to filter the list of replications on any metadata value.

Select a replication flow to perform the following tasks:

-   Display the replication in the Modeler application by selecting *Go to Monitoring* in the menu bar.
-   Select the :gear: icon to configure the following settings:
    -   *Replication Priority*: Select *High*, *Medium*, or *Low*. Selecting *High* runs this replication flow before others. The default is *Medium*.
    -   *Source Maximum Connections*: Increase or limit the number of source connections permitted to the source. The default is 10.
    -   *Target Maximum Connections*: Increase or limit the number of target connections permitted to the target. The default is 10.

-   To start the replication flow, select the <span class="SAP-icons"></span> Start Execution icon.
-   To suspend the execution of the replication flow, select the <span class="SAP-icons"></span> Suspend Execution icon.
-   To refresh the list of replication flows, select the <span class="SAP-icons"></span> Refresh icon.
-   Select a replication to display the tasks in the lower pane. Perform the following tasks in the *Tasks* area, after selecting a task:
    -   Select the :gear: icon to configure *Task Priority* for the task. For example, select *High* to run this task before others. The default is *Medium*.
    -   Select the <span class="SAP-icons"></span> Start Execution icon to run the task.
    -   Select the <span class="SAP-icons"></span> Suspend Execution icon to suspend execution of the task.
    -   Select the <span class="SAP-icons"></span> Refresh icon to refresh the list of tasks.




</td>
</tr>
</table>

**Related Information**  


[Schedule Graph Executions](../using-graphs/schedule-graph-executions-cb46d5f.md "The SAP Data Intelligence Modeler provides capabilities to schedule graph executions.")

