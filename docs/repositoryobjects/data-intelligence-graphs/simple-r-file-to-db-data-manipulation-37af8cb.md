<!-- loio37af8cb1c42e476fa5bf7176652f214f -->

# Simple R File-to-DB Data Manipulation

Exemplifies file data manipulation using plain R \(using only built-in libraries\) and writing the manipulated data to an SAP HANA database table.



<a name="loio37af8cb1c42e476fa5bf7176652f214f__section_zmq_1vc_1kb"/>

## Prerequisites

For this graph, you wil need:

-   a file containing data.

    In the preconfigured example a CSV format file `test_products.csv` is assumed to sit in the `files/exampleData/scenarioTemplates` folder. It should have a header row and contain at least the following columns "PRODUCTID", "PRODUCTNAME" and "CATEGORY".

-   a connection with ID CUSTDATAPROC\_HANA to an SAP HANA database.




<a name="loio37af8cb1c42e476fa5bf7176652f214f__section_og5_sb2_1kb"/>

## Configure and Run

Choose Run As from the Run drop-down menu and select the "default" configuration substitutions to run the graph with a preconfigured example configuration.

1.  Click on the *Script* button of the Process Data operator and enter the R code that performs the data manipulation. Consult the operator documentation for details.

    The preconfigured example script will filter for Notebooks on the column "CATEGORY" and return the columns "PRODUCTID", "PRODUCTNAME" and "CATEGORY" in the projection.

2.  Enter the path of the file containing the input data in the `Path` configuration parameter of the Read Input File operator.

    The example configuration includes `/exampleData/scenarioTemplates/test_products.csv` for this parameter \(it will prepend the `/files` prefix, matching the folder found in System Management\).

3.  Configure the database connection and the target table for the data manipulation result in the `Connection`, `Table name`, and `Table columns` configuration parameters of the Write to HANA DB operator.

    In the preconfigured example the results will be written to the *PRODUCTS\_RESULT* table in the user schema pertaining to the user of the configured SAP HANA connection. The table will be created when executing the graph.

4.  Run the graph by clicking the *Run* button.


