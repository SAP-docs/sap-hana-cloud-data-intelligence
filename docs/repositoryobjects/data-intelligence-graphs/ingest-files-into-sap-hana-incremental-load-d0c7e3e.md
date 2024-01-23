<!-- loiod0c7e3e9b0dc4e5eb485c7f675cb1d82 -->

# Ingest Files Into SAP HANA \(Incremental Load\)

With an incremental load, the SAP Data Intelligence Modeler application loads data continuously to an SAP HANA table from CSV or JSON files that are in cloud storage. The graph processes all existing files first, and then monitors the directory to load new or modified files.



The SAP HANA incremental load graph flows as follows:

-   **Monitor files:** The application monitors the configured path for new and modified files that match the `products.*\.csv` regular expression. When the graph starts, the application lists all files once because the “Already exists” event is also enabled.
-   **Reads file:** The operator receives any files that haven't been processed, reads the file contents, and sends the content to the SAP HANA client.
-   **Loads content:** The SAP HANA client loads the CSV or JSON content into the configured table, based on the table initialization configuration. If the table doesn't exist, the application creates a new table.

    > ### Caution:  
    > If the application restarts the graph, it can send files twice, which results in duplicate records. To avoid duplicate records, change the insert mode of the SAP HANA client to “`UPSERT`” and then create primary keys on the SAP HANA table.




<a name="loiod0c7e3e9b0dc4e5eb485c7f675cb1d82__section_zmq_1vc_1kb"/>

## Prerequisites

Before you run the graph, ensure that you've configured the following:

-   A connection to one of the supported cloud storages.

-   A running SAP HANA database with a matching registered connection.






### Optional Configuration

Configure the multiplicity of the graph group. Multiplicity controls the number of parallel instances in which the application reads files and loads the data into SAP HANA. For more information about multiplicity, see [Partitioning](../data-intelligence-operators/partitioning-86085d9.md).



<a name="loiod0c7e3e9b0dc4e5eb485c7f675cb1d82__section_vyv_4sh_1zb"/>

## Configure and Run the Graph

1.  In the Modeler application, open the scenario template `com.sap.scenarioTemplates.datalakeToDatabase.ingestToHana` \(Ingest Files into HANA\).
2.  Complete the `HANA_CONNECTION` value with the respective connection ID for SAP HANA.
3.  Run the graph.
4.  Optional. To see the produced data, connect to SAP HANA and browse the table `DEMO_STDL2DBHANAINGEST_PRODUCTS` under the schema you configured.

For more information about running the scenario template, see [Loading Data from Data Lake to Database (SAP HANA)](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/7eec494c03f747529cd637e2c2fd8d7c.html "These graphs show how to batch and stream process data.") :arrow_upper_right:.

