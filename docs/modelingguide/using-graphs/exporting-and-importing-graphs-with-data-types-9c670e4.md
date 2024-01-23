<!-- loio9c670e48c168462c82387bf60fb82515 -->

# Exporting and Importing Graphs with Data Types

When your graph has added data types, and you want to reuse the graph in another system, you must export and import the graph from the repository instead of copying and pasting the JSON content.



<a name="loio9c670e48c168462c82387bf60fb82515__prereq_dwq_1j5_xxb"/>

## Prerequisites

Before you perform the following steps, ensure that you complete the following tasks:

-   Create a graph: [Creating Graphs](creating-graphs/creating-graphs-aea42f8.md).
-   Create a new data type: [Create Data Types in Graph](create-data-types-in-graph-7849362.md).
-   Assigned the new data type to a port in the graph: [Use Data Types in Graph](use-data-types-in-graph-fe0f680.md).



## Context

SAP Data Intelligence adds additional subfolders to a graph structure to store a data type definition. However, the additional data type definition isn't included in the JSON content. Therefore, if you reuse a graph from one system, such as a test system, to another system, such as a production system, it's important to use the options *Export as a Solution* and *Import as a Solution*.

Perform the following steps in SAP Data Intelligence Modeler:



## Procedure

1.  Open the *Repository* tab in the navigation pane at left.

2.  Select the graph to export in the **Graphs** node.

3.  Choose *Export as solution* from the *Export selected files or folders* list at the top of the navigation pane.

    The *Export Solution* dialog opens.

4.  Complete the export by performing the following substeps:

    1.  Enter a name for the exported graph for the new environment.

        > ### Sample Code:  
        > ```
        > "name": "<graph_name>"
        > ```

    2.  Enter a version for the graph.

        > ### Sample Code:  
        > ```
        > "version": "<graph_version>"
        > ```

    3.  **Optional:** Complete the remaining attributes as necessary:

        > ### Sample Code:  
        > ```
        > ...format": "2",
        > "description": "",
        > "dependencies": [ ]
        > }
        > ```

    4.  Select *Export Solution*.


5.  To import the graph, open the target SAP Data Intelligence environment and perform the following steps in the Modeler:

    1.  Open the *Repository* tab.

    2.  Choose *Import Solution* from the *Import File* list.

    3.  Select the solution and choose *Open*.


    The imported graph appears listed in the **Graphs** node of the *Repository* tab.


