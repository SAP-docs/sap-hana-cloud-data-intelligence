<!-- loiof696fe59b6de4284b9a0e6f456709a51 -->

# Configure the Union Node

A Union node represents a relational union operation.



<a name="loiof696fe59b6de4284b9a0e6f456709a51__prereq_nmv_kzg_c1b"/>

## Prerequisites

You have configured the operator with the Union node and connected the previous nodes to Union node.



<a name="loiof696fe59b6de4284b9a0e6f456709a51__context_fct_m45_wlb"/>

## Context

The union operator forms the union from two or more inputs with the same signature. This operator can either select all values including duplicates \(UNION ALL\) or only distinct values \(UNION\).



<a name="loiof696fe59b6de4284b9a0e6f456709a51__steps_gct_m45_wlb"/>

## Procedure

1.  In the canvas, select the *Union* node.

2.  Choose ![](../using-graphs/images/Config2_1_afd8b6e.png) \(Open Configuration\).

    In the *Configuration* pane, under the *Columns* section, you can see the column information from the previous nodes.

3.  If you want to merge all of the input data \(including duplicate entries\) into one output, enable the *Union All* toggle button.

4.  Add and connect new nodes.

    If you want to configure the Data Transform operator with another node:

    1.  In the menu bar, use the breadcrumb navigation to go back to the node editor.

    2.  Add new nodes.

    3.  To connect the nodes, select the output port of a node and drag the cursor to an input port of another node.


5.  Define data target.

    It is necessary to create a data target to the node and create an output port for *Data Transform* operator.

    1.  Right-click the output port of the node and select *Create Data Target*.



