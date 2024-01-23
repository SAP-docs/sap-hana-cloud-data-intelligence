<!-- loio75c43b4808b346e1a3ffcaa1234b6733 -->

# Load Files Into SAP HANA \(Full Load\)

With a full load, the SAP Data Intelligence Modeler application loads data to an SAP HANA table from CSV or JSON files that are in cloud storage, and stops the graph after it has loaded all files.

The SAP HANA incremental load graph flows as follows:

-   **Lists files:** The application lists all files in the configured path. This operation happens only once. If there aren't files to list, the graph fails.Converts incoming data:
-   **Converts data:** The graph converts incoming data of type `message.file` to type `message`.
-   **Reads files:** The operator receives files that haven't been processed, reads its content, and sends the content to the SAP HANA client.
-   **Loads content:** The SAP HANA client loads the CSV or JSON content into the configured table, based on the table initialization configuration. If the table doesn't exist, the application creates a new table.

    > ### Caution:  
    > If the application restarts the graph, it can send files twice, which results in duplicate records. To avoid duplicate records, change the insert mode of the SAP HANA client to “`UPSERT`” and then create primary keys on the SAP HANA table.

-   **Sends signal:** The Stop Handler checks for the `message.lastBatch` header, and sends a signal to the Graph Terminator.
-   **Terminates graph:** The Graph Terminator stops the graph as completed after it receives an input.



<a name="loio75c43b4808b346e1a3ffcaa1234b6733__section_lp4_nsf_xyb"/>

## Prerequisites

Before you run the graph, ensure that you've configured the following:

-   A connection to one of the supported cloud storages.
-   A running SAP HANA database with a matching registered connection.



<a name="loio75c43b4808b346e1a3ffcaa1234b6733__section_tzr_hqh_1zb"/>

## Configure and Run the Graph

1.  In the Modeler application, open the scenario template `com.sap.scenarioTemplates.datalakeToDatabase.loadToHana` \(Load Files into HANA\).
2.  Complete the `HANA_CONNECTION` value with the respective connection ID for SAP HANA.
3.  Run the graph.
4.  Optional. To see the produced data, connect to SAP HANA and browse the table `DEMO_STDL2DBHANALOAD_PRODUCTS` under the schema you configured.

For complete information about running the scenario template, see [Loading Data from Data Lake to Database (SAP HANA)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/7eec494c03f747529cd637e2c2fd8d7c.html "These graphs show how to batch and stream process data.") :arrow_upper_right: in the *Modeling Guide*.

