<!-- loio7c6b15c197814320b960c4872a9e7f99 -->

# Using Data Types

SAP Data Intelligence uses data types for compatibility, structure, and ease of converting data types between operators.

Data types provide a strong type system for graphs \(pipelines\). Data types provide the following advantages:

-   Compatibility checks for connections between operators.
-   A structured way of specifying messages and carrying metadata through the graph.
-   Converts data types without the need for specific type converter operators.

> ### Note:  
> The Modeler stores all default data types in the *Data Types* tab in the navigation pane.



<a name="loio7c6b15c197814320b960c4872a9e7f99__section_nlz_nxh_bsb"/>

## Data Type Categories

In SAP Data Intelligence, data types have the following data type categories:


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Scalars

</td>
<td valign="top">

Primitive data types used as base for structures and tables.

> ### Example:  
> Integers, floats, strings, and dates.

Create new scalar data types only in the local scope. You can't create new scalars in the Global Scope.

</td>
</tr>
<tr>
<td valign="top">

Structures

</td>
<td valign="top">

Collection of fields where each field has a name and a value. Field names are strings, but values can be any existing scalar data type.

</td>
</tr>
<tr>
<td valign="top">

Tables

</td>
<td valign="top">

Complex data types composed of fields \(as columns\). Each field has a list of values. The fields are meant to model tabular entities that are typical of SQL databases. Each table can be interpreted as a list of similar structures. Therefore, each table field \(column\) is composed of scalars.

</td>
</tr>
</table>

You can create structure or table data types. When creating the structure data type, you need to select the scalars to compose the structure. When creating table data types, you can also define the primary key columns.



<a name="loio7c6b15c197814320b960c4872a9e7f99__section_kbl_rgc_wrb"/>

## Data Type Scopes

Data Types can have the scopes described in the following table.


<table>
<tr>
<th valign="top">

Scope

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Global

</td>
<td valign="top">

Data types that are global are accessible to any graph \(pipeline\).

</td>
</tr>
<tr>
<td valign="top">

Local

</td>
<td valign="top">

Local data types are visible only in the graph in which the data type is created.

</td>
</tr>
<tr>
<td valign="top">

Dynamic

</td>
<td valign="top">

Dynamic data types are created during runtime and exist only in memory.

> ### Note:  
> Dynamic data types are created by the operator's internal API. They're only available for the Generation 2 Python operators. In the port specification, the dynamic scope is indicated by an asterisk \(\*\) as the Data Type ID. Keep in mind the different data types are still valid. Therefore, a table can only be connected to another table port.



</td>
</tr>
</table>

> ### Note:  
> All pre-existing data types are global.

-   **[Creating Global Data Types](creating-data-types/creating-global-data-types-426f6c7.md "Extend the data type system provided by SAP Data Intelligence Modeler by creating new data types.")**  
Extend the data type system provided by SAP Data Intelligence Modeler by creating new data types.
-   **[Creating Local Data Types](creating-local-data-types-c996f5e.md "Local data types are bound to the graph in which you created them, and are visible only in the graph. ")**  
Local data types are bound to the graph in which you created them, and are visible only in the graph.

