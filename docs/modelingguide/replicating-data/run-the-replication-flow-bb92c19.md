<!-- loiobb92c1922c5a49018ef9ecf159c0937d -->

# Run the Replication Flow

Running replicates the datasets from the source to the target.



## Prerequisites

You have created a replication flow with one or more tasks and saved, validated, and deployed the replication flow to the shared repository.



<a name="loiobb92c1922c5a49018ef9ecf159c0937d__steps_vg3_gsz_gqb"/>

## Procedure

1.  Open the replication flow to run.

2.  Choose the *Run* icon in the toolbar.

    The *Activity Monitor* displays the status. You can also view the *Log* tab for processing details.

    Note that once it is running, you can suspend the execution using the toolbar button. To resume, choose *Run*. These actions are also available on the Monitoring application for both replication flows and individual tasks.




<a name="loiobb92c1922c5a49018ef9ecf159c0937d__result_jct_kdh_hqb"/>

## Results

You can now view the execution status and other details of the replication flows and tasks in the SAP Data Intelligence Monitoring application.

Note that after the target has been populated, to reload the data again follow these steps:

1.  In the Modeler, display the replication flow.
2.  Choose *Undeploy*.
3.  Choose *Deploy*.
4.  Choose *Run*.

**Related Information**  


[Monitoring SAP Data Intelligence](../dataintelligence-monitoring/monitoring-sap-data-intelligence-5413074.md "SAP Data Intelligence provides a stand-alone monitoring application to monitor the status of graphs run in the Modeler. The Monitoring application provides capabilities to visualize the summary of graphs run in the SAP Data Intelligence Modeler with relevant charts.")

