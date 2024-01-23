<!-- loio00e87feddf24478e9aa0c41495e63516 -->

# R File Data Manipulation

This graph exemplifies file data manipulation with an R custom operator and writing the manipulated data back to another file.



<a name="loio00e87feddf24478e9aa0c41495e63516__section_uht_5l2_vkb"/>

## Prerequisites

For this graph to run you will need:

-   a file containing data.

    In the preconfigured example a CSV format file `test_products.csv` is assumed to sit in the `/files/exampleData/scenarioTemplate` folder. It should have a header row and contain at least the following columns "PRODUCTID", "PRODUCTNAME" and "CATEGORY".




<a name="loio00e87feddf24478e9aa0c41495e63516__section_eqn_vk2_vkb"/>

## Configure and Run the Graph

Choose *Run As* from the *Run* drop-down menu and select the "default" configuration substitutions to run the graph with a preconfigured example configuration.

1.  To modify the data manipulation performed by the custom operator go to the *Operators* tab and find the *Process Data with R* operator, then select *Edit* from the operator's context menu.
2.  Enter the path of the file containing the input data in the *Path* configuration parameter of the Read Input File operator.

    The example configuration includes `/exampleData/scenarioTemplates/test_large.csv` for this parameter \(the operator will prepend the `/files/` prefix, matching the folder found in System Management\).

3.  Enter the file path for the data manipulation result in the *Path* configuration parameter of the Write Results File operator.

    In the preconfigured example the results will be written to a file `test_custom_r.csv` in the `/files/exampleData/scenarioTemplates` folder.

4.  Run the graph by clicking the *Run* button.

