<!-- loio88d58fd825c943c09130af49f6326d4a -->

# Simple Javascript File-to-DB Data Manipulation

Exemplifies file data manipulation using plain Javascript \(without any libraries\) and writing the manipulated data to an SAP HANA database table.



<a name="loio88d58fd825c943c09130af49f6326d4a__section_zmq_1vc_1kb"/>

## Prerequisites

For this graph, you wil need:

-   a file containing data.

    In the preconfigured example a JSON format file test\_input.json is assumed to sit in the files/exampleData/scenarioTemplates folder. It should contain an array of objects with a string type id property and some numerical data properties.

-   a connection with ID CUSTDATAPROC\_HANA to an SAP HANA database.




<a name="loio88d58fd825c943c09130af49f6326d4a__section_og5_sb2_1kb"/>

## Configure and Run

1.  Click on the Script button of the Process Data operator and enter the Javascript code that performs the data manipulation. Consult the operator documentation for details. Please note that the operator supports ECMAScript 2009 \(ES5\) specifications.

    The preconfigured example script will insert an additional row of data between each data row in the test\_input.json file that contains interpolated values for each numerical column.

2.  Enter the path of the file containing the input data in the Path configuration parameter of the Read Input File operator.

    In the preconfigured example the results will be written to a file ``test_db_js.json`` in the ``/files/exampleData/scenarioTemplates``folder.

3.  Configure the database connection and the target table for the data manipulation result in the Connection, Table name, and Table columns configuration parameters of the Write to HANA DB operator.

    In the preconfigured example the results will be written to the CUSTDATAPROC\_RESULT table in the user schema pertaining to the user of the configured SAP HANA connection. The table will be created when executing the graph.

4.  Run the graph by clicking the Run button.


