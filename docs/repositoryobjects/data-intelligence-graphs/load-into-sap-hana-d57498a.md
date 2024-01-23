<!-- loiod57498a3182d420fab888f0c78158c2f -->

# Load into SAP HANA

The data generator produces sensor data as a CSV string. The data is loaded into SAP HANA and in parallel sent to a terminal, which you can use to see the generated data.



<a name="loiod57498a3182d420fab888f0c78158c2f__section_ivl_mvb_v2b"/>

## Prerequisites

-   A running SAP HANA database.



<a name="loiod57498a3182d420fab888f0c78158c2f__section_ft5_prb_v2b"/>

## Configure and Run the Graph

1.  Right-click the SAP HANA Client operator and select *Open Configuration*. In the configuration panel, click the *Connection* property to show its editor, then fill in the values with valid connection parameters.
2.  Save the graph.
3.  In the tool bar, click the down-pointing arrow next to the *Run* button and choose *Run As*.
4.  In the dialog box, fill in the schema configuration value with a schema name that does not yet exist. The HANA Client operator will create it for you.
5.  Click *OK*.
6.  The *Status* panel indicates if the graph is running.
7.  Use the context menu *Open UI* of the *Terminal* node to open the terminal.
8.  The terminal opens and you see the produced files and their content.



### Optional Step: Check the files on HANA

1.  Connect to SAP HANA and browse the table "test" under the schema you configured to see the produced sensor data.

