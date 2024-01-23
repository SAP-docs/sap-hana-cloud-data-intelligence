<!-- loio4080eec5ff86431d85ae087cf39ba29f -->

# Monitoring Graphs

After creating and running graphs, monitor graphs and view statistics.

The following table describes the options for monitoring the graph status in the SAP Data Intelligence Modeler.


<table>
<tr>
<th valign="top">

Action

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Monitor Status of Graph Runs

</td>
<td valign="top">

After you create and run a graph, monitor the status of the graph run in the Modeler.

Use the standalone monitoring application that SAP Data Intelligence provides to monitor the status of all graphs executed in the Modeler.

</td>
</tr>
<tr>
<td valign="top">

Trace Messages

</td>
<td valign="top">

Trace messages monitor both the system and running graphs to isolate problems or errors that may occur. Trace messages provide an initial analysis of your running graphs so you can troubleshoot potential problems or errors.

</td>
</tr>
<tr>
<td valign="top">

Use SAP Data Intelligence Monitoring

</td>
<td valign="top">

SAP Data Intelligence provides the Monitoring application to monitor the status of graphs run in the SAP Data Intelligence Modeler.

</td>
</tr>
<tr>
<td valign="top">

Access the SAP Data Intelligence Monitoring Query API

</td>
<td valign="top">

Access the SAP Data Intelligence Monitoring Query API to retrieve application performance metrics for your tenant. For more information, see [Accessing the SAP Data Intelligence Monitoring Query API](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/9bc60ac178964f23b3fee513595a73a4.html "Tenant administrators can access the SAP Data Intelligence Monitoring Query API to retrieve tenant application performance metrics from the Prometheus monitoring service running in an SAP Data Intelligence cluster.") :arrow_upper_right:.

</td>
</tr>
<tr>
<td valign="top">

SAP Data Intelligence Diagnostics

</td>
<td valign="top">

SAP Data Intelligence Diagnostics deploys one of the most widely used stacks of open-source monitoring and diagnostic tools for Kubernetes. For health and performance monitoring, SAP Data Intelligence Diagnostics provides cluster administrators access to cluster-wide system and application metrics.

</td>
</tr>
</table>



> ### Note:  
> Developer member users with the sap.dh.monitoring policy can monitor the status of graph runs for all tenant users.

> ### Note:  
> By default, the Modeler also performs logging. The log messages are intended for a broader audience with different skills. If you want to view the log messages, start the Modeler, and in the bottom pane, select the *Logs* tab.

-   **[Monitor the Graph Execution Status](monitor-the-graph-execution-status-610a01b.md "After creating and executing a graph, you can monitor the status of the graph execution in the SAP Data Intelligence application.")**  
After creating and executing a graph, you can monitor the status of the graph execution in the SAP Data Intelligence application.
-   **[Activate Trace Messages](activate-trace-messages-5916711.md "Trace message logs contain a complete set of information for monitoring graph execution performance. Trace message logs help you to
		isolate problems or errors that occur based on different severity threshold levels.  ")**  
Trace message logs contain a complete set of information for monitoring graph execution performance. Trace message logs help you to isolate problems or errors that occur based on different severity threshold levels.
-   **[Downloading Diagnostic Information for Graphs](downloading-diagnostic-information-for-graphs-3d966fe.md "To help you diagnose graph issues, download a zipped archive of information.")**  
To help you diagnose graph issues, download a zipped archive of information.

