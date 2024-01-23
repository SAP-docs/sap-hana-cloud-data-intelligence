<!-- loio8eb832407a794de3a000ee37da67c167 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Structured SQL Consumer

SQL Consumer operator reads from a specified database using native SQL. This operator produces a structured output, and you need to connect it to other operators from Structured Data Operators category.



<a name="loio8eb832407a794de3a000ee37da67c167__steps_stg_qqx_jlb"/>

## Procedure

1.  Start the SAP Data Intelligence Modeler.

2.  In the navigation pane, select the *Graphs* tab.

3.  Choose :heavy_plus_sign: \(Create Graph\).

    The application opens an empty graph editor in the same window, where you can define your graph. A graph can contain a single operator or a network of operators based on the business requirement.

4.  In the *Operators* tab, double-click the *Structured SQL Consumer* operator \(or drag and drop it to the graph editor\) to add it as a process in the graph.

5.  To open the editor of the *Structured SQL Consumer* operator, double-click the operator.

6.  Configure the Service and Connection properties.

7.  Write an SQL statement in the *SQL Editor* dialog.

8.  In the graph editor, select the operator and choose ![](../using-graphs/images/Config2_1_afd8b6e.png) \(Open Configuration\) to define the other required configurations of the operator in the configuration panel.

9.  Add any producer operator form the Strutured Data Operators category to the graph.

10. Connect the output port of the *Structured SQL Consumer* operator to the producer operator.

11. To control the stop of the graph execution, add the Graph Terminator operator at the end of the graph.

12. Connect the output port of the producer operator to the Graph Terminator operator.

13. Save and execute the graph.


