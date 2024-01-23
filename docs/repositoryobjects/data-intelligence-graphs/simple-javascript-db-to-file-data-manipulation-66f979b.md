<!-- loio66f979b6bc834639860f7440555f245a -->

# Simple Javascript DB-to-File Data Manipulation

Exemplifies the manipulation of data from an SAP HANA database table using plain Javascript \(without any libraries\) and writing the manipulated data to a file.



<a name="loio66f979b6bc834639860f7440555f245a__section_zmq_1vc_1kb"/>

## Prerequisites

For this graph, you wil need:

-   a connection with ID CUSTDATAPROC\_HANA to an SAP HANA database.

-   a database table in SAP HANA containing data.

    In the preconfigured example a table CUSTDATAPROC\_RESULT is assumed to exist in the user schema pertaining to the user of the CUSTDATAPROC\_HANA SAP HANA database connection. It should contain a string type ID column and some numerical data columns. A table like this is created by running the com.sap.scenarioTemplates.customDataProcessing.simpleF2DBJavascript graph.




<a name="loio66f979b6bc834639860f7440555f245a__section_og5_sb2_1kb"/>

## Configure and Run

1.  Choose Run As from the Run drop-down menu and select the "default" configuration substitutions to run the graph with a preconfigured example configuration.

2.  Enter the SQL statement that reads the input data from the SAP HANA database table in the Content configuration parameter of the SQL Statement operator.

    The example configuration contains select \* from CUSTDATAPROC\_RESULT order by ID for this parameter.

3.  Choose the connection for the input data in the Connection configuration parameter of the Get Data from DB operator.

    In the example configuration this parameter is set to CUSTDATAPROC\_HANA.

4.  Click on the Script button of the Process Data operator and enter the Javascript code that performs the data manipulation. Consult the operator documentation for details. Please note that the operator supports ECMAScript 2009 \(ES5\) specifications.

    The preconfigured example script will insert an additional row of data between each data row in the CUSTDATAPROC\_RESULT table that contains interpolated values for each numerical column.

5.  Enter the file path for the data manipulation result in the Path configuration parameter of the Write Results File operator.

    In the preconfigured example the results will be written to a file ``test_db_js.json`` in the ``/files/exampleData/scenarioTemplates`` folder.

    Run the graph by clicking the Run button.


