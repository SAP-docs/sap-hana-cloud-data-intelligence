<!-- loio0857b43d3aed46b0a8d2f7b82c2cbd30 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Validate Graphs

Graph validation is an automatic or manual process that analyzes a graph for correct structure and components, such as operators, ports, groups, and configuration.

The results of a graph validation show that the graph analyses are successful. Graph validation checks the following components of a graph:

-   Graph configuration
-   Operator connections
-   Tag configuration for groups defined in a graph
-   Graph resource requests and limits

Validation doesn't build the graph with the corresponding resources and dependencies. Therefore, validation doesn't take as long as running the graph.



<a name="loio0857b43d3aed46b0a8d2f7b82c2cbd30__section_m25_1c5_45b"/>

## Types of Graph Validation

There are two types of graph validation based on when the validation is performed:

-   **Implicit validation:** Performed when you save or run a graph. Implicit validation is also known as automatic validation.
-   **Explicit validation:** Performed when you start graph validation manually. Explicit validation is also known as manual validation.

    Start an explicit validation by selecting the <span class="SAP-icons"></span> \(Validate\) icon in the *Data Intelligence Modeler* editor toolbar.




<a name="loio0857b43d3aed46b0a8d2f7b82c2cbd30__section_ngv_vb5_45b"/>

## View Validation Results

To view graph validation results, open the *Validation* tab in the bottom pane of the *Data Intelligence Modeler*. It displays either a success message or a list of errors and warnings.

-   Success: The graph doesn't have any warnings or errors.
-   Warning: There's a problem with the graph. This problem won't cause the graph to fail, but it can result in other issues later.
-   Error: There's an issue with the graph. This problem will cause the graph to fail and needs to be fixed.

    > ### Note:  
    > If validation finds any errors or warnings, you can fix some of the issues by selecting the <span class="SAP-icons"></span> \(help\) icon located to the right of the error or warning message.


When the validation results in errors, you can't run the graph until you fix the errors and revalidate the graph.

-   **[Graph Validation Warnings and Errors](graph-validation-warnings-and-errors-72d5fa1.md "When a graph validation isn't successful, the Data Intelligence Modeler creates a list of warnings and errors, with a link to additional
		information about the warning or error. ")**  
When a graph validation isn't successful, the Data Intelligence Modeler creates a list of warnings and errors, with a link to additional information about the warning or error.

