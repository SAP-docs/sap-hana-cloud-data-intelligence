<!-- loio546a90242b11488aa16d2e209f64b8bf -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Structured File Consumer

Structured File Consumer operator reads from any supported cloud storage. The operator produces structured output, and you need to connect it to other operators from Structured Data Operators category.



<a name="loio546a90242b11488aa16d2e209f64b8bf__steps_stg_qqx_jlb"/>

## Procedure

1.  Start the SAP Data Intelligence Modeler.

2.  In the navigation pane, select the *Graphs* tab.

3.  Choose :heavy_plus_sign: \(Create Graph\).

    The application opens an empty graph editor in the same window, where you can define your graph. A graph can contain a single operator or a network of operators based on the business requirement.

4.  In the *Operators* tab, double-click the *Structured File Consumer* operator \(or drag and drop it to the graph editor\) to add it as a process in the graph.

5.  To open the editor of the *Structured File Consumer* operator, double-click the operator.

6.  Configure the Service, Connection, and Source \(dataset\) properties.

    -   For CSV files, you can define various CSV properties.
    -   For JSON files, you can mention the flattening level in the JSON properties.
    -   For directories containing part-files, you can select the partition type and choose what happens upon string truncation.

7.  Delete columns or define filters to orchestrate the data as required.

    > ### Note:  
    > -   Use the *Data Preview* option to see the original data from the source or to see the configured data. If the table is very wide or contains a number of large column types, the result may be truncated in order to avoid out of memory issues.
    > -   The file browsing and data preview is not possible if substitution parameters are used to configure the connection ID or the table name properties.

8.  In the graph editor, select the operator and choose ![](../using-graphs/images/Config2_1_afd8b6e.png) \(Open Configuration\) to define the other required configurations of the operator in the configuration panel.

9.  Add any producer operator form the Strutured Data Operators category to the graph.

10. Connect the output port of the *Structured File Consumer* operator to the producer operator.

11. To control the stop of the graph execution, add the Graph Terminator operator at the end of the graph.

12. Connect the output port of the producer operator to the Graph Terminator operator.

13. Save and execute the graph.


-   **[Consuming Excel Files with Structured File Consumer Operator](consuming-excel-files-with-structured-file-consumer-operator-bbba1be.md "Use a structured file consumer operator and select an Excel file as a source in a pipeline to transform the Excel format to a table or
		dataset.")**  
Use a structured file consumer operator and select an Excel file as a source in a pipeline to transform the Excel format to a table or dataset.

