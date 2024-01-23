<!-- loio591671120f6f4b1db87d050c2e9ed036 -->

# Activate Trace Messages

Trace message logs contain a complete set of information for monitoring graph execution performance. Trace message logs help you to isolate problems or errors that occur based on different severity threshold levels.



<a name="loio591671120f6f4b1db87d050c2e9ed036__prereq_b3z_ps5_cxb"/>

## Prerequisites

Read about trace levels in [Trace Severity Levels](trace-severity-levels-34cad34.md).



## Context

You can activate trace message logging to find errors that occur sporadically. The Modeler logs the trace messages and categorizes them based on the severity levels. You can also limit the number of trace files that are written at the same time.

Trace messages are intended for specific users. For example, trace messages are useful for users with development skills and a deep understanding of the Modeler to debug graph executions.





## Procedure

1.  Start the SAP Data Intelligence Modeler application.

2.  Open the *Trace* tab in the graph's runtime view.

    In the *Trace* tab, you can configure the trace level, download the latest logs, and monitor the trace messages for different severity levels.

3.  **Optional:** To change the group and trace level, perform the following substeps:

    By default, a graph's *Trace Level* is INFO.

    1.  Select *Group: default | Trace Level: INFO* at the top right of the *Trace* tab.

    2.  In the *Trace Configuration* dialog, select a different value from the *Trace Level* list.

        Trace Level options are as follows:

        -   INFO
        -   DEBUG
        -   ERROR
        -   FATAL
        -   WARNING

    3.  Select *OK*.


4.  **Optional:** Select *Get Latest Logs* at the top right of the *Trace* tab.

    The Modeler displays the latest logs.


-   **[Trace Severity Levels](trace-severity-levels-34cad34.md "When streaming the traces for the SAP Data Intelligence
		Modeler application, you can set a trace severity threshold. Depending on the trace level
		that you define, the application streams messages accordingly into the trace
		server.")**  
When streaming the traces for the SAP Data Intelligence Modeler application, you can set a trace severity threshold. Depending on the trace level that you define, the application streams messages accordingly into the trace server.

