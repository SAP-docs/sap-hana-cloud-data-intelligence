<!-- loio426f6c7e602d44a295184124becd8e73 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Creating Global Data Types

Extend the data type system provided by SAP Data Intelligence Modeler by creating new data types.



<a name="loio426f6c7e602d44a295184124becd8e73__prereq_apr_vp3_rvb"/>

## Prerequisites

Before you create data types, ensure that you understand the concepts of data type category, scope, and compatibility. For complete information about data types, see [Using Data Types](../using-data-types-7c6b15c.md) and [Data Types in Operator Ports](../using-operators/data-types-in-operator-ports-9fa7d06.md).



<a name="loio426f6c7e602d44a295184124becd8e73__context_ld5_ncb_2lb"/>

## Context

You can create global data types in addition to the data types provided by SAP Data Intelligence. The system also creates dynamic data types during runtime that are applicable only for the Generation 2 Python operators.

The following steps are for creating global data types.

There are three data types: Scalar, structure, and table:

-   The scalar data types are predefined.
-   You can define structure and table data types.

To create structure or table data types, perform the following steps:



<a name="loio426f6c7e602d44a295184124becd8e73__steps_qzn_5h2_blb"/>

## Procedure

1.  Start the SAP Data Intelligence Modeler.

2.  In the navigation pane, choose the *Data Types* tab.

    If you don't see the *Data Types* tab, select the <span class="SAP-icons"></span> \(Additional Tabs\) icon at the bottom of the tab list and select *Data Types*.

3.  In the navigation pane toolbar, choose :heavy_plus_sign: .

    The *Create Data Type* dialog box opens.

4.  Enter a name for the data type in the *ID* text box.

    The name must be two or more identifiers separated by a period \(.\).

5.  Choose either *Structure* or *Table* for the *Type*.

6.  Select *OK*.

    The data type editor opens in the workspace area.

7.  Select :heavy_plus_sign:in the *Properties* box.

    Data types can have more than one property.

    Property parameters appear to the right of the *Properties* box.

8.  If you select *Structure*, complete the properties by performing the following substeps:

    1.  Enter a name for the new property in the *Name* text box.

    2.  Choose a global scalar data type from the *Scalar Type ID* list.

        Scalars compose the structure.


9.  If you select *Table*, complete the properties by performing the following substeps:

    1.  Enter a name for the new property in the *Name* text box.

    2.  Choose a global scalar data type from the *Scalar Type ID* list.

    3.  Switch the *Key Property* toggle to on to make this data type the primary key column.


10. Select :floppy_disk:.

    You can save an instance of the data type after you save it by selecting *Save As* from the *Save* list.

    The data types are stored in a tree structure in the *Data Types* tab.

11. **Optional:** To edit structure or table data type, double-click the data type in the tree view of the navigation pane.

12. **Optional:** To delete a data type, right-click the data type in the tree view of the navigation pane and choose *Delete*.


