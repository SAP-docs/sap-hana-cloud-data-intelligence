<!-- loio00c6e4b79c6d4f1a87d0d1e5effef0fb -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# SAP Application Consumer

The SAP Application Consumer operator allows you to create pipelines that consume data from SAP and non-SAP sources as modeled in the Pipeline Modeler, and connect them to other structured operators such as the Structured Data Transform operator.



<a name="loio00c6e4b79c6d4f1a87d0d1e5effef0fb__steps_stg_qqx_jlb"/>

## Procedure

1.  Start the SAP Data Intelligence Modeler.

2.  In the navigation pane, select the *Graphs* tab.

3.  Choose :heavy_plus_sign: \(Create Graph\).

    The application opens an empty graph editor in the same window, where you can define your graph. A graph can contain a single operator or a network of operators based on the business requirement.

4.  In the *Operators* tab, double-click the *SAP Application Consumer* operator \(or drag and drop it to the graph editor\) to add it as a process in the graph.

5.  To open the editor of the *SAP Application Consumer* operator, double-click the operator.

6.  Configure the Service, Connection, and Source \(dataset\) properties. You can delete columns or define filters to orchestrate the data as required.

    -   For directories containing part-files, you can select the partition type and choose what happens upon string truncation.
    -   For OData service, you can browse and expand the navigation properties by defining the *Depth* value based on which the *Source Columns* section is updated. The depth value can be either 1 or 2.

    > ### Note:  
    > -   Use the *Data Preview* option to see the original data from the source or to see the configured data. If the table is very wide or contains a number of large column types, the result may be truncated in order to avoid out of memory issues.
    > -   The file browsing and data preview is not possible if substitution parameters are used to configure the connection ID or the table name properties.

7.  In the graph editor, select the operator and choose ![](../using-graphs/images/Config2_1_afd8b6e.png) \(Open Configuration\) to define the other required configurations of the operator in the configuration panel.

8.  Add any producer operator from the Structured Data Operators category to the graph.

9.  Connect the output port of the *SAP Application Consumer* operator to the producer operator.

10. To control the stop of the graph execution, add the Graph Terminator operator at the end of the graph.

11. Connect the output port of the producer operator to the Graph Terminator operator.

12. Save and execute the graph.


