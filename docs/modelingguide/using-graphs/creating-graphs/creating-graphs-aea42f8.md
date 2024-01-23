<!-- loioaea42f8cf13740f8af59b8cb89939147 -->

<link rel="stylesheet" type="text/css" href="../../css/sap-icons.css"/>

# Creating Graphs

A graph \(pipeline\) consists of operators that you configure to form a specific process and connect using input and output ports.



<a name="loioaea42f8cf13740f8af59b8cb89939147__prereq_emp_pmk_35b"/>

## Prerequisites

SAP Data Intelligence Modeler provides Generation 1 \(Gen1\) and Generation 2 \(Gen2\) operators. Before you create a graph, determine which group of operators to use. You can build a graph using either Gen1 or Gen2 operators, but you can't combine them in a single graph. For complete information about Gen1 and Gen2 operators, see [Generation 1 and Generation 2 Operators](../../using-operators/generation-1-and-generation-2-operators-1c97a10.md).

A graph can contain a single operator, or a network of operators based on the purpose of the graph.



<a name="loioaea42f8cf13740f8af59b8cb89939147__context_vtx_r5j_rvb"/>

## Context

To create a basic graph, open the Modeler application and perform the following steps:



## Procedure

1.  In the navigation pane at left, open the *Graphs* tab.

2.  Select the down arrow next to :heavy_plus_sign: and choose either *Use Generation 1 Operators* or *Use Generation 2 Operators*.

    The Modeler opens the *Operators* tab. The tab lists only the operators belonging to the generation you selected. The Modeler also opens an empty graph editor to the right of the navigation pane. Use the graph editor area to create the graph.

    > ### Tip:  
    > The Modeler groups the operators in the *Operators* tab under specific categories. To customize the list of operators, use the <span class="SAP-icons"></span> \(Customize Visible Categories\) icon or use the *Search* bar.
    > 
    > For more information about operator types and categories, see the *Repository Objects Reference*.

3.  Double-click the first operator for your graph in the *Operators* tab.

    The Modeler adds the operator to the graph editor workspace. Add additional operators as necessary in the same manner.

4.  Each operator has default configuration settings. You can change default settings or create additional configuration parameters. To configure each operator based on its purpose, perform the following substeps:

    1.  Select the operator in the graph editor workspace.

    2.  Select <span class="SAP-icons"></span> \(Show Configuration\) next to the operator.

        The Modeler opens a *Configuration* pane at right. Based on the operator type, you can also specify values for the subengine configuration parameters.

    3.  Configure each operator in your graph in the same manner.


    For more information about operator configuration settings, see the *Repository Objects Reference*.

5.  **Optional:** Select *Validate* in the *Configuration* pane.

    If the operator has a type scheme associated with it, then validate the configuration parameters' values against the conditions defined in the schema. For example, validate mandatory fields, minimum or maximum length, value formats, regular expression, and so on.

    > ### Note:  
    > The validation is based on the constraints defined in the scheme. The Modeler validates all configuration parameter values and displays validation errors, if any.

6.  Connect the operators: Drag and drop your cursor from the output port of one operator to an input port of another operator.

    Continue connecting the operators in your graph so that all operators are connected in the order in which to process the data. The Modeler helps you select the allowable input port type by highlighting all input ports based on the output port type.

7.  **Optional:** To configure the graph, perform the following substeps:

    1.  Ensure that no individual object in the graph is selected, then select <span class="SAP-icons"></span> \(Show Configuration\).

    2.  Complete the parameters as described in the following table.


        <table>
        <tr>
        <th valign="top">

        Parameter
        
        </th>
        <th valign="top">

        Description
        
        </th>
        </tr>
        <tr>
        <td valign="top">
        
        *Description*
        
        </td>
        <td valign="top">
        
        Enter a description of the graph.
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        *Icon file name*
        
        </td>
        <td valign="top">
        
        Enter the icon name, such as `kafka.png`.
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        *Icon*
        
        </td>
        <td valign="top">
        
        Enter the Font Awesome icon name, or choose an option from the list.

        The Modeler uses the icon for display only when you don't provide a value for *Icon file name*.
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        *Disable lineage*
        
        </td>
        <td valign="top">
        
        Slide the toggle to ON or OFF.

        Applicable only for graphs that contain certain operators that support lineage extraction. You can use the Metadata Explorer tool to view data lineage.
        
        </td>
        </tr>
        </table>
        

8.  Choose *Save* from the :floppy_disk:list.

9.  Enter the fully qualified path and file name for the graph in *Name*, and optionally enter a description in *Description*.

10. Choose the applicable value from the *Category* list, or enter a new category.

11. Select *OK*.

    The Modeler saves the graph and operators in a folder structure in the modeler repository, such as <code>...com/sap/others/<i class="varname">&lt;graphname&gt;</i></code>. To save another instance of the graph, in the editor bar, choose *Save As* from the :floppy_disk: list and provide the applicable information in the *Save* dialog box.

12. **Optional:** To export the graph to the JSON definition after you create and save the graph, perform the following substeps:

    1.  Open the *Graphs* tab in the navigation pane at left.

    2.  Right-click the applicable graph and choose *Export*.


    The Modeler creates the JSON file and places it in your Downloads folder.


**Related Information**  


 <?sap-ot O2O class="- topic/link " href="217dac1ce21c46d6956208d3d699f596.xml" text="" desc="" xtrc="topicref:11" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiofafe266fc7664785bb84cb7ab4822a2e_en-US/src/content/localization/en-us/cc6d420f2462481ebf668f705ee32f9e.ditamap" ?> 

[SAP Data Intelligence Operators](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/acd32810819a4b2893c9f8698e2ec55c.html "SAP Data Intelligence provides built-in operators, that you can use directly in a graph or as the basis for creating a custom operator.") :arrow_upper_right:

[Creating Operators](../../using-operators/creating-operators-049d2f3.md "Use the SAP Data Intelligence Modeler to create your own operators to use in graphs (pipelines).")

[Monitor the Graph Execution Status](../monitor-the-graph-execution-status-610a01b.md "After creating and executing a graph, you can monitor the status of the graph execution in the SAP Data Intelligence application.")

