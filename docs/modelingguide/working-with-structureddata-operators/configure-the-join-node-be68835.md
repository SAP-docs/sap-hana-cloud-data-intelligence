<!-- loiobe6883549a7a4db8a6138b011b82e486 -->

# Configure the Join Node

A Join node represents a relational multiway join operation.



<a name="loiobe6883549a7a4db8a6138b011b82e486__prereq_rgf_nvt_tdb"/>

## Prerequisites

You have configured the operator with the Join node and connected output of one or two previous nodes to the Join node.



<a name="loiobe6883549a7a4db8a6138b011b82e486__context_ujz_wzp_f1b"/>

## Context

The Join node can perform multiple step joins on maximum of two inputs. Configure the Join node to define the join condition and the output columns of the Join node.

> ### Note:  
> The Join node is not available for real-time processing.



<a name="loiobe6883549a7a4db8a6138b011b82e486__steps_gpt_5sx_jlb"/>

## Procedure

1.  Double-click the *Join* node.

2.  Create a join.

    1.  In the *Definition* tab, select a source.

    2.  Choose ![](images/Create_Join_SDH_8ce0e13.png) \(Create Join\) and drag the cursor to another source on the canvas with which you want to create a join.

        You can also create a join by selecting a column in the source and dragging the cursor to the required column in a different source. In this case, the application automatically creates a join condition.


3.  Define the join.

    The *Join Definition* pane, define the join type and the join condition.

    1.  In the *Join Type* dropdown list, select a value.


        <table>
        <tr>
        <th valign="top">

        Join Type
        
        </th>
        <th valign="top">

        Description
        
        </th>
        </tr>
        <tr>
        <td valign="top">
        
        Inner Join
        
        </td>
        <td valign="top">
        
        Use when each record in the two tables has matching records.
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        Left Outer
        
        </td>
        <td valign="top">
        
        Outputs all records in the left table, even when the join condition does not match any records in the right table.
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        Right Outer
        
        </td>
        <td valign="top">
        
        Outputs all records in the right table, even when the join condition does not match any records in the left table.
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        Cross
        
        </td>
        <td valign="top">
        
        Outputs all possible combinations of rows from the two tables.
        
        </td>
        </tr>
        </table>
        
    2.  In the expression editor, enter a join condition.

    3.  **Optional:** To use the join condition that the application proposes, select *Propose Condition*.

        The application analyzes the sources participating in the join and proposes a condition.


4.  Define the output columns.

    In the *Columns* tab, define the output columns of the join node.

    1.  In the toolbar, choose the *Columns* tab.

    2.  In the *Mapping* pane, select a *Source* column and drag and drop it into the *Drop row here* zone in the *Target* section.

        > ### Note:  
        > You can also duplicate an output column \(map the same source column more than once\). Select the required *Source* column and hold and drag the cursor to the *Drop row here* zone in the *Target* section.

    3.  **Optional:** If you want to automatically map the columns based on column names, in the *Source* section, choose ![](images/AutoMapNew_1a399c3.png) \(Auto Map by Name\).

    4.  If you want to edit a column name, select a *Target* column and choose ![](../using-graphs/images/Edit1_01244d0.png) \(Edit\).

        > ### Note:  
        > You cannot edit the data type of output columns of a join node.

    5.  If you want to remap an output column with a different source column, right-click the mapping and choose *Remap*.

        Select a new source column and choose *OK*.


5.  **Optional:** Reorder output columns.

    In the *Columns* tab toolbar, switch to the *Form* pane to reorder the output columns.

    1.  To reorder the columns, select the column that you want to move and in the toolbar click the up or down arrows.


6.  Add and connect new nodes.

    If you want to configure the Data Transform operator with another node:

    1.  In the menu bar, use the breadcrumb navigation to go back to the node editor.

    2.  **Optional:** Add new nodes.

    3.  To connect the nodes, select the output port of a node and drag the cursor to an input port of another node.


7.  Define data target.

    It is necessary to create a data target to the node and create an output port for Data Transform operator.

    1.  Right-click the output port of the node and select *Create Data Target*.



-   **[Join Design Considerations](join-design-considerations-93c128e.md "You can control memory and CPU usage used to process joins, improve runtime performance of the joins in the graph, and process more joins
		within a graph effectively with resource limitations.")**  
You can control memory and CPU usage used to process joins, improve runtime performance of the joins in the graph, and process more joins within a graph effectively with resource limitations.

