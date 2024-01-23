<!-- loio6b7d6b485faf433a8efc792c099fb218 -->

# Configure the Case Node

The Case node specifies multiple paths so that the rows are separated and processed in different ways.



<a name="loio6b7d6b485faf433a8efc792c099fb218__prereq_nmv_kzg_c1b"/>

## Prerequisites

You have defined the operator with a Case node and connected the previous node to the Case node.



## Context

Route input records from a single source to one or more output paths. You can simplify branch logic in data flows by consolidating case or decision making logic in one node. Paths are defined in an expression table. By default, there are two output ports defined. The one ending in *Default* contains any records that do not meet the expression definition in one of the other output ports.



## Procedure

1.  Double-click the *Case* node.

2.  **Optional:** Select *Output Row Once* to specify whether a row can be included in only one or many output targets.

    For example, you might have a partial address that does not include a country name such as 455 Rue de la Marine. It is possible that this row could be output to the tables named `Canada_Customer`,`France_Customer`, and `Other_Customer`. Select this option to output the record into the first output table whose expression returns TRUE. Not selecting this option would put the record in all three tables.

3.  **Optional:** Choose *\+* \(Add Port\) to add more Case output ports and expressions.

4.  Click the name under the *Output Port Name* heading to rename the port to be more meaningful. For example, Canada\_Customer.

5.  Click the link under the *Expression* heading to open the expression editor.

6.  In the expression editor, define an expression for the records that you want to include in this output.

7.  Define the default port by selecting the required output port and choose *Default*.

    The default port contains any records that do not meet the expression definition in one of the other output ports.

8.  Add and connect new nodes.

    If you want to configure the Data Transform operator with another node:

    1.  In the menu bar, use the breadcrumb navigation to go back to the node editor.

    2.  Add new nodes.

    3.  To connect the nodes, select the output port of a node and drag the cursor to an input port of another node.


9.  Define data target.

    It is necessary to create a data target to the node and create an output port for *Data Transform*

    1.  Right-click the output port of the node and select *Create Data Target*.


    operator.


