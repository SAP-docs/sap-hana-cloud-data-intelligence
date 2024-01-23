<!-- loio4bf172bcbdc543a59fbad729f5dfd7db -->

# Automatic Graph Recovery

Configure any graph to recover from failure automatically, regardless of whether the graph uses Generation 1 or Generation 2 operators.

When *Automatic Recovery* is enabled in the *Run As* dialog, the runtime system monitors the graph for failures and maintains a failure counter. As long as the failure counter is lower than the set options in the *Recovery Configuration* group, the runtime system restarts the graph with the same runtime configuration. If the graph fails within the set retry time, the error counter is reset.

> ### Note:  
> Early graph failures are often caused for only temporary reasons, such as initial network or resource allocation timeouts. By resetting the failure counter, you prevent unintentional consumption of the automatic retrials.

The following table describes the options in the *Recovery Configuration* group.


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

*Automatic Recovery*

</td>
<td valign="top">

Select to turn on automatic recovery.

</td>
</tr>
<tr>
<td valign="top">

*Retry for *<n\>* run\(s\)*

</td>
<td valign="top">

Specifies the number of runs for which to retry the graph before the counter is reset.

</td>
</tr>
<tr>
<td valign="top">

*within the threshold value of *<n\>* second\(s\)*

</td>
<td valign="top">

Specifies the time limit for retrying the graph before the counter is reset.

</td>
</tr>
</table>



<a name="loio4bf172bcbdc543a59fbad729f5dfd7db__section_qqr_kz5_vrb"/>

## Finally Failed Graphs

When the number of retries exceeds the settings in the *Recovery Configuration* group, the graph finally fails and the automatic restart feature stops. However, a finally failed graph can still be restarted manually at any time, even if the trials have been exceeded.

> ### Note:  
> The number for automatic restart trials can't be changed once the graph has started.



<a name="loio4bf172bcbdc543a59fbad729f5dfd7db__section_yjv_pz5_vrb"/>

## Run Graph with Automatic Recovery

To enable the automatic recovery, check the option *Automatic Recovery* in the *Run As* dialog. To reset the failure counter, complete the *Recovery Configuration* group options.

The following table describes the details that appear in the *Overview* tab in the Modeler after the graph has entered the running state.


<table>
<tr>
<th valign="top">

Detail

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Status

</td>
<td valign="top">

The current status of the graph.

</td>
</tr>
<tr>
<td valign="top">

Runtime Handle

</td>
<td valign="top">

The ID of the current running graph graph. Every run has a unique ID.

</td>
</tr>
<tr>
<td valign="top">

Restart ID

</td>
<td valign="top">

The ID of the automatic recovery configuration. All recovered graph runs share the same Restart ID.

</td>
</tr>
<tr>
<td valign="top">

Run Order

</td>
<td valign="top">

Indicates how often the graph has been recovered. Because the graph can also be restarted manually, the Run Order can exceed the Maximum Automatic Retries.

</td>
</tr>
<tr>
<td valign="top">

Current Failure Counter

</td>
<td valign="top">

Shows how often the graph has failed. You can reset this counter if recovery fails within the set retry threshold time.

</td>
</tr>
<tr>
<td valign="top">

Run Type

</td>
<td valign="top">

Shows whether the graph has been recovered automatically or restarted manually.

</td>
</tr>
<tr>
<td valign="top">

Maximum Automatic Retries

</td>
<td valign="top">

The number of retries.

</td>
</tr>
<tr>
<td valign="top">

Retry Threshold Time

</td>
<td valign="top">

The threshold time for resetting the current failure counter for early failures.

</td>
</tr>
</table>

> ### Example:  
> ```
> 
> Retry Threshold Time: 30s
> Maximum Automatic Retries: 3
> 
> Instance: 0
> Graph running for: 40s
> Increase current failure count: false
> Current failure count: 0
> 
> Instance: 1
> Graph running for: 20s
> Increase current failure count: true
> Current failure count: 1
> 
> Instance: 2
> Graph running for: 31s
> Increase current failure count: false
> Current failure count: 0
> 
> Instance: 3
> Graph running for: 20s
> Increase current failure count: true
> Current failure count: 1
> 
> Instance: 4
> Graph running for: 28s
> Increase current failure count: true
> Current failure count: 2
> 
> Instance: 5
> Graph running for: 15s
> Increase current failure count: true
> Current failure count: 3
> 
> Maximum retries reached
> ```



<a name="loio4bf172bcbdc543a59fbad729f5dfd7db__section_yyp_l4f_cvb"/>

## The Status Tab

The *Status* tab lists all graph runs. The *Status* tab has two views, linear list and tree view that groups all runs belonging to the same automatic restart configuration \(automatic restart group\).

You can perform the following tasks in the *Status* tab:

-   Download diagnostics information.
-   Pause and restart the graph run.
-   Archive the graph run.



<a name="loio4bf172bcbdc543a59fbad729f5dfd7db__section_xgd_s1v_vrb"/>

## Automatic Graph Recovery and System Maintenance

When the system changes to maintenance mode, all graphs eligible for automatic restart enter the “stopped by pause” state. After the system goes back to production mode and the pipeline modeler is running for the respective users, the system restarts the graphs in the “stopped by pause” state automatically.

> ### Note:  
> The automatic restart is triggered only when the user who owns that graph logs on to the system and starts the pipeline modeler.



<a name="loio4bf172bcbdc543a59fbad729f5dfd7db__section_ddh_qr1_vvb"/>

## Pause and Stop Graphs Manually

Use the options in the *Status* tab to manually pause, restart, and stop graphs. Pausing and restarting graphs is helpful when you develop and test recoverable graphs.

> ### Note:  
> Paused graphs keep allocating resources. If you don't plan to later restart a paused graph, SAP recommends stopping the graph to free resources.

You can restart a graph that has a status of “stopped by pause” at any time.

You can stop a graph manually, or the system stops the graph automatically when it completes its work. When a graph is stopped, it enters the state of “completed” and can't be restarted or recovered.



<a name="loio4bf172bcbdc543a59fbad729f5dfd7db__section_s3w_rr1_vvb"/>

## Archiving Graphs

You can archive a graph when it enters into any of the following states:

-   “completed”
-   “stopped by pause”
-   “dead”

> ### Restriction:  
> To prevent potential data loss, a graph can't be archived when it's in the “stopped by pause” state and has a valid snapshot.

**Parent topic:**[Running Graphs](running-graphs-439d0a0.md "After creating a graph, you can run the graph based on the configuration defined for the graph. The Modeler application runs the operators in the graph as individual processes.")

**Related Information**  


[Parameterize the Graph Run Process](parameterize-the-graph-run-process-f3caf16.md "Parameterize the graph run process using parameters that assume different values based on the values passed in each graph run.")

[Debug Graphs](debug-graphs-06b0159.md "You can start the graph in debug mode to verify the input and output from each operator during execution and analyze or modify the data passing through a connection.")

[Schedule Graph Executions](schedule-graph-executions-cb46d5f.md "The SAP Data Intelligence Modeler provides capabilities to schedule graph executions.")

[Managing Cluster Hibernation and Wakeup](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/911eae13fc4849db8b3b237a91a86d04.html#loio911eae13fc4849db8b3b237a91a86d04 "To reduce costs while your SAP Data Intelligence clusters aren't in use, you can "pause" cluster nodes.") :arrow_upper_right:

