<!-- loio45d5d5d514934448a2614937a75fc23b -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# SAP Application Producer

The SAP Application Producer operator allows you to create pipelines that write data to SAP Business Warehouse and OData targets as modeled in the Pipeline Modeler, and connect them to other structured operators such as the Structured Data Transform operator.



<a name="loio45d5d5d514934448a2614937a75fc23b__steps_stg_qqx_jlb"/>

## Procedure

1.  Start the SAP Data Intelligence Modeler.

2.  In the navigation pane, select the *Graphs* tab.

3.  Choose :heavy_plus_sign: \(Create Graph\).

    The application opens an empty graph editor in the same window, where you can define your graph. A graph can contain a single operator or a network of operators based on the business requirement.

4.  In the *Operators* tab, double-click the *SAP Application Producer* operator \(or drag and drop it to the graph editor\) to add it as a process in the graph.

5.  Add any consumer operator from the Structured Data Operators category to the graph. To know more about configuring consumer operators, See [Structured Consumer Operators](structured-consumer-operators-abd02a9.md).

6.  Connect the output port of the consumer operator to the *SAP Application Producer* operator.

7.  To open the custom editor of the *SAP Application Producer* operator, double-click the operator.

8.  Configure the Service, Connection, and Target properties. You can map source and target columns if not automatically mapped.

    > ### Note:  
    > -   Use the *Data Preview* option to see the output data. If the table is very wide or contains a number of large column types, the result may be truncated in order to avoid out of memory issues.
    > -   The file browsing and data preview is not possible if substitution parameters are used to configure the connection ID or the table name properties.

9.  In the graph editor, select the operator and choose ![](../using-graphs/images/Config2_1_afd8b6e.png) \(Open Configuration\) to define the other required configurations of the operator.

10. To control the stop of the graph execution, add the Graph Terminator operator at the end of the graph.

11. Connect the output port of the producer operator to the Graph Terminator operator.

12. Save and execute the graph.


