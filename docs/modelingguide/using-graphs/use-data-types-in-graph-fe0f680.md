<!-- loiofe0f680ebbc545bb9aecb94dab30eaed -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Use Data Types in Graph



## Procedure

1.  In the navigation pane, choose the *Graphs* tab.

2.  In the navigation pane bar, choose :heavy_plus_sign: \(Create Graph\).

    The application opens an empty graph editor in the same window, where you can define your graph.

3.  In the navigation pane, choose the *Operators* tab.

4.  Choose source and target operators that supports addition of ports from the *Structured Data Operators* category.

5.  In the context menu of the source, select the *Add Port* option.

6.  Do the following in *Add Port* dialog:

    1.  Enter the output port name

    2.  Select data type as Structure, Table, or Scalar

    3.  Select a data type name from the value help, and click *OK*.


7.  Drag from this port to the target operator.

    If there’s a port of compatible data type, the connection is created to this port. Else, a new input port is created on the target operator and is connected. If the port doesn’t allow additional ports, the link to the operator is not created.

    > ### Restriction:  
    > Only structured data transform operator supports data types.


