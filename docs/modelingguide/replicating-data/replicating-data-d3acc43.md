<!-- loiod3acc43c77c848b6a82d899ff6895f99 -->

# Replicating Data

SAP Data Intelligence replication flows let you transfer small or large datasets, in batch or real-time, from a source to a target using full or delta loading.

You create a replication flow by first configuring source and target connections. Then add one or more tasks, each of which consists of a source object, its corresponding target, and any associated configuration options such as filters or custom mappings. Finally, save it in your user space.



## Deploying and Undeploying Replication Flows

After creating and validating a replication flow, you deploy it to the shared \(tenant\) repository, where you can run it. Deployment also makes the replication flow available to other users of the tenant for viewing, importing, or modification.

You can undeploy your replication flow for various reasons, such as:

-   You want to delete that replication flow from the shared repository because it no longer needs to be run.

-   You wish to modify the replication flow and redeploy it.

Undeploying deactivates the flow from the replication service and performs some housekeeping of the connected source system and of runtime artifacts of the replication service within SAP Data Intelligence Cloud. For more specific details, see [Undeploy a Replication Flow](undeploy-a-replication-flow-4e7d434.md).

The SAP Data Intelligence Monitoring application provides an interface where you can view and manage replication flow and task processes.

> ### Note:  
> To see the known limitations of the replication flow functionality in SAP Data Intelligence, see SAP Note [3223810](https://me.sap.com/notes/3223810).



## Possible Duplication of Records

If you use replication flows with any target system, the data replication process provides "at-least-once delivery". Therefore, duplicate change records may be delivered to the target system, which results in eventual consistency when the replication is recovering the data load in error situations.

However, when the target system is a database \(such as HANA Cloud\), the duplicates are eliminated during the replication execution by using the UPSERT mechanism of the databases, thereby providing "exactly-once delivery".

For other targets—for example, Amazon Web Service Storage Services \(S3\), Microsoft Azure Data Lake Storage Gen2 \(ADL\_V2\), Google Cloud Service \(GCS\), or HANA Data Lake \(HDL\) file, use *Suppress Duplicates* to minimize the occurrence of duplicates during the initial load. For more information about duplicate suppression, see [Create a Replication Flow](create-a-replication-flow-a425e34.md).

For duplicate records that can't be automatically eliminated in the target cloud storage, use the information provided in the timestamp column to help you identify the currently valid record and ignore potential duplicated records.

Also note that because source rows may be sent multiple times in an effort to maintain data consistency, the replication may present a replication row count that is greater than the actual rows in the target.

-   **[Create a Replication Flow](create-a-replication-flow-a425e34.md "The SAP Data Intelligence
		Modeler includes an interface for creating and running replication flows. ")**  
The SAP Data Intelligence Modeler includes an interface for creating and running replication flows.
-   **[Validate the Replication Flow](validate-the-replication-flow-c716063.md "Validation ensures the minimum requirements have been specified for the replication flow
		for deployment and execution.")**  
Validation ensures the minimum requirements have been specified for the replication flow for deployment and execution.
-   **[Deploy the Replication Flow](deploy-the-replication-flow-c0d5528.md "Deploy the replication flow to enable its execution.")**  
Deploy the replication flow to enable its execution.
-   **[Run the Replication Flow](run-the-replication-flow-bb92c19.md "Running replicates the datasets from the source to the target.")**  
Running replicates the datasets from the source to the target.
-   **[Cloud Storage Target Structure](cloud-storage-target-structure-12e0f97.md "Running a replication flow with a cloud storage target creates various files and
        structures.")**  
Running a replication flow with a cloud storage target creates various files and structures.
-   **[Kafka as Target](kafka-as-target-b9b819c.md "In a replication flow, every source dataset is transferred to a respective topic in
		the Kafka cluster.")**  
In a replication flow, every source dataset is transferred to a respective topic in the Kafka cluster.
-   **[ABAP Cluster Table Replications with Delta Load](abap-cluster-table-replications-with-delta-load-69319bb.md "Replications from ABAP cluster tables result in more complex operations on the target
		system if delta load is involved.")**  
Replications from ABAP cluster tables result in more complex operations on the target system if delta load is involved.
-   **[Edit an Existing Replication Flow](edit-an-existing-replication-flow-3cb5d3f.md "You can import, edit, and update replication flows that have been deployed by you or
		other users to the shared repository.  ")**  
You can import, edit, and update replication flows that have been deployed by you or other users to the shared repository.
-   **[Undeploy a Replication Flow](undeploy-a-replication-flow-4e7d434.md "You can undeploy an SAP Data Intelligence
		replication flow (remove it from the shared repository) using the Replications editor in the SAP Data Intelligence Modeler.")**  
You can undeploy an SAP Data Intelligence replication flow \(remove it from the shared repository\) using the Replications editor in the SAP Data Intelligence Modeler.
-   **[Delete a Replication Flow](delete-a-replication-flow-0205d8c.md "Delete SAP Data Intelligence replication flows or their associated tasks using the
			Replications editor in the Modeler interface. ")**  
Delete SAP Data Intelligence replication flows or their associated tasks using the *Replications* editor in the Modeler interface.
-   **[Clean Up Source Artifacts](clean-up-source-artifacts-599586b.md "Some situations, such as when an administrator deletes a tenant or connection, can
		result in unused source artifacts that you need to delete to avoid performance
		issues.")**  
Some situations, such as when an administrator deletes a tenant or connection, can result in unused source artifacts that you need to delete to avoid performance issues.

**Related Information**  


[Monitoring SAP Data Intelligence](../dataintelligence-monitoring/monitoring-sap-data-intelligence-5413074.md "SAP Data Intelligence provides a stand-alone monitoring application to monitor the status of graphs run in the Modeler. The Monitoring application provides capabilities to visualize the summary of graphs run in the SAP Data Intelligence Modeler with relevant charts.")

[Replication Flow Connections](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/f4327d3e2f7146a19e76924f8a79454a.html "The following tables list the data source and target systems supported by the replication management service in SAP Data Intelligence. This service manages the replication functionality (replication flows) in the SAP Data Intelligence Modeler application.") :arrow_upper_right:

