<!-- loioac09193393934b44b731a2b77e9ad590 -->

# Simple R File Data Manipulation

This graph exemplifies file data manipulation using plain R \(using only built-in libraries\) and writing the manipulated data back to another file.



<a name="loioac09193393934b44b731a2b77e9ad590__section_gdy_mrx_zkb"/>

## Prerequisites

For this graph, you wil need:

-   a file containing data.

    In the preconfigured example a CSV format file `test_products.csv` is assumed to sit in the `/files/exampleData/scenarioTemplates` folder. It should have a header row and contain at least the following columns "PRODUCTID", "PRODUCTNAME" and "CATEGORY".




<a name="loioac09193393934b44b731a2b77e9ad590__section_n2y_vyw_zkb"/>

## Configure and Run

Choose *Run As* from the *Run* drop-down menu and select the "default" configuration substitutions to run the graph with a preconfigured example configuration.

1.  Click on the *Script* button of the **Process Data** operator and enter the R code that performs the data manipulation. Consult the operator documentation for details.

    The preconfigured example script will filter for Notebooks on the column "CATEGORY" and return the columns "PRODUCTID", "PRODUCTNAME" and "CATEGORY" in the projection.

2.  Enter the path of the file containing the input data in the `Path` configuration parameter of the **Read Input File** operator.

    The example configuration includes `/exampleData/scenarioTemplates/test_products.csv` for this parameter \(the operator will prepend the `/files/` prefix, matching the folder found in System Management\).

3.  Enter the file path for the data manipulation result in the `Path` configuration parameter of the **Write Results File** operator.

    In the preconfigured example the results will be written to a file `test_result_products_transformed.csv` in the `/files/exampleData/scenarioTemplates` folder.

4.  Run the resulting graph by clicking the *Run* button.

