<!-- loioc996f5e17a3d4ee8b17fcdf5cf210cf0 -->

<link rel="stylesheet" type="text/css" href="css/sap-icons.css"/>

# Creating Local Data Types

Local data types are bound to the graph in which you created them, and are visible only in the graph.



<a name="loioc996f5e17a3d4ee8b17fcdf5cf210cf0__prereq_apr_vp3_rvb"/>

## Prerequisites

Before you create data types, ensure that you understand the concepts of data type category, scope, and compatibility. For complete information about data types, see [Using Data Types](using-data-types-7c6b15c.md) and [Data Types in Operator Ports](using-operators/data-types-in-operator-ports-9fa7d06.md).



## Context

You can create local data types in addition to global and the data types provided by SAP Data Intelligence. The system also creates dynamic data types during runtime that are applicable only for the Generation 2 Python operators.

To create a local data type, perform the following steps in the Modeler:



## Procedure

1.  Open the applicable pipeline.

2.  Select <span class="SAP-icons"></span> \(Show configuration\).

    Make sure that none of the operators in the graph are selected when you select Show configuration.

3.  Expand the Data Types section in the *Configuration* panel.

4.  Select :heavy_plus_sign:

    The *Create Data Type* dialog box opens.

5.  Enter a name for the data type in the *ID* text box.

    The name must start with an alphabet and can consist of a string with alphabets, digits, or underscores.

6.  Choose either *Structure*, *Table*, or *Scalar* for the *Type*.

    You can choose *Scalar* only for local data types.

7.  If you chose *Structure* or *Table*, perform the following substeps:

    1.  Enter a description for the new data type.

    2.  Add one or more properties to the new data type.

    3.  Select *Save*.


8.  If you chose *Scalar*, perform the following substeps:

    1.  Enter a description for the new data type.

    2.  Select a template from the Template list.

    3.  Select *Save*.



