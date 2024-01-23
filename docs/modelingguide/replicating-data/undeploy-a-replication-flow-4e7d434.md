<!-- loio4e7d434ceddb4dc68f47ef9ac1e26f85 -->

# Undeploy a Replication Flow

You can undeploy an SAP Data Intelligence replication flow \(remove it from the shared repository\) using the Replications editor in the SAP Data Intelligence Modeler.



## Context

You may want to undeploy replication flows for different reasons:

-   You want to change the configuration of your existing replication flow; for example, to change the target data set or to apply a filter to a task.
-   You want to reset or reinitialize a replication flow, including all of its associated tasks, and remove dependent artifacts on the connected source system.

You can undeploy a replication flow that is available in your personal user repository from the SAP Data Intelligence shared repository by using the Undeploy icon in the modeling screen. Note that the undeploy action can only be executed for replication flows that are already activated or running.

If you undeploy a replication flow, the system stops any running initial load or delta process for this task and it deletes certain runtime objects that belong to your replication flow, but it does not delete the target table even if the replication management system created the target table.



## Procedure

1.  To undeploy a replication flow from your user repository, start the SAP Data Intelligence Modeler.

2.  In the navigation pane, choose the *Replications* tab.

3.  Choose the replication flow in the list of available replication flows.

4.  Click the *Undeploy* button available on the top menu bar.

5.  In the confirmation dialog, click *OK* to continue with the undeploy action.

    > ### Note:  
    > When undeploying a replication flow that copies data from a connected source system \(for example: SAP S/4HANA, SAP System via SLT, or Azure SQL\), this removes the subscription to the source table from the source system, which includes the triggers and logging tables. This applies to all of the source systems, including SAP S/4HANA and relational databases, such as Azure SQL. In the case of SAP S/4HANA, the undeploy action also removes the dependent runtime artifacts related to replication when the undeployment process is successfully executed.
    > 
    > In order to not block the undeployment process indefinitely, SAP Data Intelligence retries three times to successfully undeploy each task in a replication flow. Due to connection failure to source systems or some other unexpected reasons, SAP Data Intelligence may not be able to successfully execute the undeployment process in the source system. In case of an error during the undeployment process, it can happen that not all dependent artifacts are deleted in the connected source system. Despite the error, SAP Data Intelligence still deletes the definition of the replication flow, including its runtime data, status, and metrics from its repository in order to complete undeployment requests and allow users to proceed with completing the task of remodeling the replication flow. In this case, see [Clean Up Source Artifacts](clean-up-source-artifacts-599586b.md).


