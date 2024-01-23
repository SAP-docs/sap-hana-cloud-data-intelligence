<!-- loio246b5dcfaa6244aaa3cc8429a42d10cd -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Creating Graph Snippets

You can create your own graph snippet if you don't find a suitable one in the available list of graph snippets.



<a name="loio246b5dcfaa6244aaa3cc8429a42d10cd__steps_dvd_sk3_vkb"/>

## Procedure

1.  Start the SAP Data Intelligence Modeler.

2.  In the navigation pane, select the *Graphs* tab.

3.  In the navigation pane bar, search for an existing graph or select :heavy_plus_sign: 

4.  To create a graph snippet, select a part of the graph that you want to add as a graph snippet and right-click the selected area.

    -   Press [Shift\] and drag the mouse to select a specific part of the graph.
    -   Choose [ctrl\] + [a\]  to select the complete graph.

5.  Select the *Create Snippet* option in the context menu.

    > ### Note:  
    > If your graph snippet consists of ABAP operators, you must select the connection and version for the operator before creating the snippet.

6.  In the *Create Graph Snippet* dialog, for each operator or group, do one of the following:

    -   Select the properties that are to be configured during import of the graph snippet.
    -   Preconfigure some of the properties.

7.  **Optional:** To provide better context about the parameters during import of the graph snippet to a graph:

    1.  Click *Add Description* for a selected parameter.

    2.  Provide details about the property and click *Save*.


8.  To define parameters for properties and use across several operators, perform the following substeps:

    1.  Click *Add Parameter*.

    2.  Provide the details for the parameter and click *Save*. A parameter is created and you can use this for similar properties in other operators.

        > ### Note:  
        > -   To clear the changes you made to all operators in the graph snippet, click *Reset All*.
        > -   To view all existing parameters in the graph snippet, click *Show Parameters*.


9.  When you have finished configuring all required properties, click *Create*.

10. In the *Save Snippet* dialog, provide the necessary information for the graph snippet.

11. Click *Save*.

    The graph snippet is created. You can now import the graph snippet that you created.


