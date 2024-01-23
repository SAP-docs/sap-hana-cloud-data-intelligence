<!-- loiobde149c10dfc437f9e09d40c6be3fb2b -->

# ABAP Operators General Concepts

Use the ABAP operators to access data in ABAP-based remote systems from SAP Data Intelligence.



The ABAP operators have several general concepts that are common to some or all of the ABAP operators. The following sections describe the general concepts. For operator-specific information, see the descriptions of the individual operators in this reference guide.

For more information about the integration of data from ABAP-based SAP systems in SAP Data Intelligence, see the SAP Note [2890171](https://me.sap.com/notes/2890171), “SAP Data Intellligence/SAP Datasphere - ABAP Integration”.



<a name="loiobde149c10dfc437f9e09d40c6be3fb2b__section_qkm_b3z_rnb"/>

## Authorizations

The user specified in the ABAP connection needs authorizations for the operator and the data that is selected. For more information about authorizations, see SAP Note [2981615](https://me.sap.com/notes/2981615). This authorization concept is valid as of the following releases:

-   DMIS 2011 SP20

-   DMIS 2018 SP05
-   SAP S/4HANA Cloud 2102
-   SAP S/4HANA 2020 FPS01

For older releases, see SAP Note [2831756](https://me.sap.com/notes/2831756) “SAP Data Intelligence/SAP Datasphere - ABAP Integration Security Settings”.



<a name="loiobde149c10dfc437f9e09d40c6be3fb2b__section_hzt_k3z_rnb"/>

## Versioning

The versioning concept for ABAP operators started with SAP Data Intelligence 3.0 and SAP Data Intelligence Cloud 2003. It's possible that each operator is available in more than one version. For example, SAP ships a new version when an operator gets a new output type or is equipped with additional features. Find a list of new operator versions and their features in the SAP Note for the corresponding DMIS SP or SAP S/4HANA release. For version information, see Section 5, Release information in SAP Note [2890171](https://me.sap.com/notes/2890171), “SAP Data Intellligence/SAP Datasphere - ABAP Integration”.

This versioning concept applies only to ABAP operators, and it's different than other types of operators in SAP Data Intelligence. In SAP Data Intelligence, there's only one version of each ABAP operator because the ABAP operators in SAP Data Intelligence are just shells. The actual operators are in the ABAP-based system. SAP Data Intelligence pulls the operators from the system when needed. Therefore, if your ABAP-based source system doesn’t meet the prerequisites to provide the latest operator versions, the system doesn't list the latest ABAP operator versions in the most recent version of the Modeler for SAP Data Intelligence.

> ### Example:  
> To have the most recent version of the operators in DMIS 2011 SP17, SAP Data Intelligence requires an upgrade to the latest DMIS version.

As a rule, use the latest version that is available in the connected SAP system. However, it's also possible to continue working with an older version for consistency reasons.

For more information about the differences between available ABAP operator versions, see the **New Features** section in the specific ABAP operator description. To find out which configuration parameters are relevant for a version of an operator, see the **Relevant in Version** column in the table of configuration parameters for the operator.



<a name="loiobde149c10dfc437f9e09d40c6be3fb2b__section_izg_zkz_rnb"/>

## Subscriptions - Resume Operator Run With Subscriptions

The subscription feature for Versions V1 and V2 of the following ABAP operators allows you to resume running a graph containing these operators after the graph has stopped, whether automatically or manually:

-   ABAP CDS Reader
-   ABAP ODP Reader
-   SLT Connector

For details about the availability of the subscription feature, see the individual ABAP operator descriptions.

To start a graph that includes one of these operators for the first time, choose subscription type *New* and enter a unique name for the subscription. The system then automatically creates a technical ID \(subscription ID\) for this subscription in the ABAP-based source system. For example, the subscription ID is needed to follow up on technical issues with a subscription.

When a graph is stopped, you can restart the data load process by resuming the graph: you change the subscription type to *Existing* and choose the subscription ID for the subscription name you entered when starting the graph for the first time.

> ### Note:  
> In some cases, resuming the data load process at exactly the point where it stopped is impossible. Resuming the data load process in this manner can result in missing or duplicate records in the target environment.

As a rule, SAP Data Intelligence doesn't delete a subscription and its subscription ID automatically. To remove a subscription and its subscription ID, remove the subscription manually. For exceptions to this rule, see the individual operator descriptions. After you delete a subscription, you can't resume the related data load.

Every time a graph is stopped, the system finds and deletes subscriptions whose graphs haven't been updated for 30 days or longer. To adjust the default value for the retention period, in transaction SM30, open the maintenance view for table DHBAS\_CONFIG \(or LTBAS\_CONFIG for DMIS\) and either create a new value or overwrite the existing value for the parameter SUBSCR\_RETENTION\_IN\_DAYS.

> ### Note:  
> Because of user interface limitations, when you resume a graph with an existing subscription, SAP Data Intelligence doesn't fill the fields dynamically with the corresponding values. However, when the graph runs again, SAP Data Intelligence uses the available values for the subscription.

For steps to remove the subscription, see  <?sap-ot O2O class="- topic/xref " href="c11f62a2bc7f4d36acae80a1d829d8a7.xml" text="" desc="" xtrc="xref:1" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/bde149c10dfc437f9e09d40c6be3fb2b.xml" ?> .

-   **[ABAP CDS Reader](abap-cds-reader-df331fc.md "Use the ABAP CDS Reader operator to read data from a CDS view. ")**  
Use the ABAP CDS Reader operator to read data from a CDS view.
-   **[ABAP Converter](abap-converter-d58c19e.md "Use the ABAP Converter operator to convert a generic ABAP data type to string using the CSV, JSON, or XML format.")**  
Use the ABAP Converter operator to convert a generic ABAP data type to string using the CSV, JSON, or XML format.
-   **[ABAP ODP Reader](abap-odp-reader-d4c18f8.md "Use this operator to read data from an object for operational data processing (ODP object). ")**  
Use this operator to read data from an object for operational data processing \(ODP object\).
-   **[Cluster Table Splitter](cluster-table-splitter-aefc6b9.md "Use the Cluster Table Splitter to replicate one or more (but not all) logical tables for a cluster table.")**  
Use the Cluster Table Splitter to replicate one or more \(but not all\) logical tables for a cluster table.
-   **[Custom ABAP Operator](custom-abap-operator-bd79a31.md "You can create your own custom operators in your ABAP-based remote system. To make these operators available in SAP Data Intelligence, use
		the Custom ABAP Operator. The Custom ABAP Operator adapts dynamically to the custom operator that you select in the remote system.")**  
You can create your own custom operators in your ABAP-based remote system. To make these operators available in SAP Data Intelligence, use the Custom ABAP Operator. The Custom ABAP Operator adapts dynamically to the custom operator that you select in the remote system.
-   **[SAP ABAP Operator](sap-abap-operator-8895172.md "Use the SAP ABAP Operator to make a standard operator implementation from your ABAP-based remote system available in SAP Data
		Intelligence. The SAP ABAP Operator dynamically adapts to the selected operator in the remote system.")**  
Use the SAP ABAP Operator to make a standard operator implementation from your ABAP-based remote system available in SAP Data Intelligence. The SAP ABAP Operator dynamically adapts to the selected operator in the remote system.
-   **[SLT Connector](slt-connector-ac5b713.md "Use the SLT Connector operator to establish a connection between SAP Landscape Transformation Replication Server (SLT) and SAP Data Intelligence.")**  
Use the SLT Connector operator to establish a connection between SAP Landscape Transformation Replication Server \(SLT\) and SAP Data Intelligence.

