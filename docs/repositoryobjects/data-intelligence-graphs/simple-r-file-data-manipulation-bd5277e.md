<!-- loiobd5277e9e5a74c11950578ef4ac7f6e2 -->

# Simple R File Data Manipulation

Exemplifies file data manipulation using plain R \(using only built-in libraries\) and writing the manipulated data back to another file.



<a name="loiobd5277e9e5a74c11950578ef4ac7f6e2__section_zmq_1vc_1kb"/>

## Prerequisites

For this graph, you wil need:

-   a file containing data.

    In the preconfigured example a CSV format file ``test_products.csv`` is assumed to sit in the ``/files/exampleData/scenarioTemplates`` folder. It should have a header row and contain at least the following columns "PRODUCTID", "PRODUCTNAME" and "CATEGORY".




<a name="loiobd5277e9e5a74c11950578ef4ac7f6e2__section_og5_sb2_1kb"/>

## Configure and Run

1.  Choose Run As from the Run drop-down menu and select the "default" configuration substitutions to run the graph with a preconfigured example configuration.

2.  Click on the Script button of the Process Data operator and enter the R code that performs the data manipulation. Consult the operator documentation for details.

    The preconfigured example script will filter for Notebooks on the column "CATEGORY" and return the columns "PRODUCTID", "PRODUCTNAME" and "CATEGORY" in the projection.

3.  Enter the path of the file containing the input data in the Path configuration parameter of the Read Input File operator.

    The example configuration includes``/exampleData/scenarioTemplates/test_products.csv`` for this parameter \(the operator will prepend the ``/files/`` prefix, matching the folder found in System Management\).

4.  Enter the file path for the data manipulation result in the Path configuration parameter of the Write Results File operator.

    In the preconfigured example the results will be written to a file ``test_result_products_transformed.csv`` in the ``/files/exampleData/scenarioTemplates`` folder.

5.  Run the graph by clicking the Run button.


