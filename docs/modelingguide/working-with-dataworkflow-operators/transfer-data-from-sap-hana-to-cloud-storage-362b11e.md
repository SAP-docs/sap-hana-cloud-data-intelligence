<!-- loio362b11e4dc9249f09ed789257ac65716 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Transfer Data from SAP HANA to Cloud Storage

Use the Data Transfer operator in a graph to transfer data from an SAP HANA system to an SAP Vora system or to cloud storage.



<a name="loio362b11e4dc9249f09ed789257ac65716__prereq_ot5_5yl_vdb"/>

## Prerequisites

-   Create a connection to an SAP HANA system using the SAP Data Intelligence Connection Management application.
-   Create a connection to a cloud storage using the SAP Data Intelligence Connection Management application.



<a name="loio362b11e4dc9249f09ed789257ac65716__steps_s1p_bjv_fhb"/>

## Procedure

1.  Start the SAP Data Intelligence Modeler.

2.  Open the *Graphs* tab in the navigation pane.

3.  Select :heavy_plus_sign: in the navigation pane toolbar.

4.  Choose *Use Generation 1 Operators*.

5.  Add The Data Transfer operator to a graph.

    A graph can contain a single operator or a network of operators based on the business requirement.

    1.  Open the *Operators* tab in the navigation pane.

    2.  Enter “Data Transfer” in the search text box in the navigation toolbar.

    3.  Double-click the Data Transfer operator in the search results to add the operator as a process to the graph editor.


6.  Define the source for data transfer.

    1.  In the graph editor, double-click the *Data Transfer* operator.

        The Modeler opens an editor in the graph editor pane where you define the source and target for data transfer.

    2.  Open the *Source* tab.

        In the *Source* tab, provide details of the source dataset for the transfer operation.

    3.  Enter or browse for the applicable connection ID in the *Connection ID* text box.

        The connection ID provides the connection to an SAP HANA system.

    4.  Select <span class="SAP-icons"></span> \(Browse\) in the *Table Name* field and select the required SAP HANA table.

        The Modeler populates the connection details automatically based on the selected data set.


7.  **Optional:** Browse the Metadata Catalog and import the applicable SAP HANA table.

    1.  Select *Import Dataset* in the *Source* tab toolbar.

    2.  Browse for and select the applicable data set.

    3.  Select *OK*.

        The Modeler populates the connection details automatically based on the selected data set. For more information about the Metadata Catalog, see the *Data Governance User Guide*.


8.  Provide values to parameters.

    If the selected SAP HANA objects are defined with parameters, then it's necessary to provide values to those parameters. The application automatically populates the default values, if any, that are already defined for the parameters.

    1.  Select the *Edit* icon in the *Variables* text box and provide applicable values.

    2.  Select the variable and operator type, and provide the required values in the *Provide Parameter Values* dialog box.

    3.  **Optional:** To view only required parameters, select <span class="SAP-icons"></span> \(Add Filter\) and select *Show Mandatory Only*.


9.  Select applicable columns from the target dataset to load to the target.

    1.  Open the *Target* tab.

        The Column Mapping section lists all columns from the selected source.

    2.  Drag and drop applicable columns to the Target pane.

        > ### Note:  
        > When you map columns from source to target, or if there are pre-existing target objects that have the data types listed below, the Modeler reorders the columns in the target pane automatically based on those data types regardless of the target type.
        > 
        > The columns with the following data types appear at the end of the list in the target pane:
        > 
        > -   BLOB
        > -   CLOB
        > -   NCLOB
        > -   BINARY
        > -   VARBINARY
        > -   TEXT
        > -   BINTEXT


10. **Optional:** Filter column values in the source dataset to load only filtered values to the target.

    > ### Remember:  
    > You can define filters only after you map columns to the target.

    1.  Open the *Source* tab.

    2.  Select :pencil2: in the *Filters* text box.

    3.  Select applicable columns in *Provide Filter Values* dialog and define the filter condition.

    4.  Select *OK*.


11. Define the cloud storage target table.

    1.  Open the *Target* tab.

    2.  Enter or browse for the connection ID for the cloud storage dataset in the *Connection ID* text box.

    3.  Enter or browse for the path to the cloud storage dataset in the *Target* text box.

        If the selected connection has a root path specified in the connection definition, then the content of this field is relative to this path.


12. Map source columns to the target columns.

    1.  Open the *Target* tab.

    2.  Drag and drop each source column in the Source pane to the corresponding target column in the Target pane in the Column Mapping section.


13. After you've mapped all of the source columns to the target columns, preview data in the columns.

    1.  Open the *Source* tab.

    2.  Select one of the following options from the *Data Preview* list:

        -   *Source Data*: Input variable values to preview the remote dataset.

            > ### Note:  
            > The variable values that you enter don't overwrite the existing values of the data transfer operator.

        -   *Adapted Data*: Preview the columns that you selected in the *Target* tab, the variable values, and the filters that you set.

    3.  To view data in the target table columns, open the *Target* tab and select *Data Preview*.

        > ### Note:  
        > When you run the data transfer, only the mapped columns are loaded to the target dataset.


14. Save and run the graph.

    You can control the start and stop of the graph run using the Workflow Trigger and Workflow Terminator operators respectively.

    > ### Tip:  
    > You can also schedule the graph execution. For more information, see [Schedule Graph Executions](../using-graphs/schedule-graph-executions-cb46d5f.md).


