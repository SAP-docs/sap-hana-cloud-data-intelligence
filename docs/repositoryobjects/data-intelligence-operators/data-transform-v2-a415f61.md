<!-- loioa415f61f6fc54043847dd3800018bf61 -->

# Data Transform V2

The Data Transform operator in Modeler provides a wide variety of options available to meet your data transformation needs. Supported in Generation 2 graphs.



Use this operator to perform data transformations, such as projection, filter, column operations, and join. It can connect with other operators that have a table port type. Such ports must have a Data Type ID defined during modeling time.



<a name="loioa415f61f6fc54043847dd3800018bf61__section_sq1_nf3_vdb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

definition

</td>
<td valign="top">

object

</td>
<td valign="top">

The definition of a transformation pipeline.

outputs: The schema is derived from the out schema of the previously connected transform.

inputs: The input schemas of the transformation pipelines. The schema is derived from the source dataset.

nodes: The transformation operations.

tablemappings: Schema mappings among inputs and outputs.

</td>
</tr>
</table>

> ### Note:  
> -   The configuration parameters for the Data Transform operator are node-specific. For more information on how to configure individual nodes in the operator, see [Data Transform](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/8fe8c0209652437994d5a79f5b95b361.html "The Data Transform operator in the SAP Data Intelligence Modeler provides wide variety of options to meet your data transformation needs.") :arrow_upper_right:.
> -   Any unconnected output port results in a graph failure.



<a name="loioa415f61f6fc54043847dd3800018bf61__section_y14_tnt_j4b"/>

## Case Transform

Specifies multiple paths in a single node. The rows are separated and each group is processed in different ways. The case transform simplifies branch logic in data flows by consolidating case or decision-making logic in one transform. Paths are defined in an expression table.

Data inputs: Only one data flow source is allowed.

Case condition expressions: Create two or more case condition expressions. Choose one as the default expression to contain the remaining records when all other case expressions evaluate to false.



<a name="loioa415f61f6fc54043847dd3800018bf61__section_g1g_14t_j4b"/>

## Union

Combines incoming datasets, producing a single output dataset with the same schema as the input datasets.

Data inputs: Two data flow sources are allowed.

Options: Choose Union All when you want to merge all of the records. To remove any duplicate records, do not select this option.



<a name="loioa415f61f6fc54043847dd3800018bf61__section_o1b_f4t_j4b"/>

## Join Design Considerations

-   Control resource usage to process JOIN in the graph – Memory and CPU
-   Improve runtime performance of the JOINs in the graph
-   Process more JOINs within a graph effectively with resource limitations



### Join Resource and Performance Control Options

When designing JOIN within a structured data transform operator, there are 2 options available: RANK and CACHE. Use these options to help control the resource needed.

-   Rank: A number whose value decides which table is considered as inner and outer. The higher rank table is outer and lower rank table is inner.
-   Cache: Indicates whether a table is cached or let the engine decide \(automatic\).



### Choosing Rank/Cache values for Join

-   DB: Database source
-   File: Cloud file source
-   Any: Any output within data transform operation like projection or join.

One source is referred as left and other one is right.



### Inner Join

**DB and DB**

-   Use lower rank for bigger table, high rank for small table
-   Cache = no for both sources

> ### Note:  
> Index must be defined for join columns on the DB table.

Runtime performance option: If the index is not defined for the inner table, choose Cache=Yes. This setting improves runtime performance but affects memory. Choose this option when there are few resource-consuming transforms.

**File and DB, Any and DB**

-   Use lower rank for DB, high rank for File
-   Cache = no for both sources

> ### Note:  
> Index must be defined for join columns on the DB table.

Runtime performance option: When the number of database rows is smaller than the file, use a lower rank for file and set Cache=Yes. This setting improves runtime performance but affects memory. Choose this option when there are few resource-consuming transforms.

**File and File, Any and File, Any and Any**

-   Use lower rank for smaller source
-   Cache = yes for lower rank source

Runtime performance option: When the number of rows is smaller in one source than another source, use a lower rank for the larger source and set Cache=Yes. This setting improves runtime performance but affects memory. Choose this option when there are few resource-consuming transforms.



### Left Outer Join

When using the LEFT OUTER JOIN, the left source is always chosen as outer, irrespective of type and the right is inner. So, the RANK value does not matter.

-   Cache = no for left table
-   Cache = no when right table is DB, Cache = yes when right table is File or Any

Runtime performance option: When the number of rows is smaller in one source than another source, use the smaller source as the LEFT \(outer\). This setting improves runtime performance but affects memory. Choose this option when there are few resource-consuming transforms.

When the RIGHT table is a database, choose Cache=No. When the RIGHT table is a File or Any, choose Cache=Yes.

> ### Note:  
> Index must be defined for join columns on the DB table.



### Right Outer Join

When using a RIGHT OUTER JOIN, the right source is always chosen as outer – irrespective of type and the left is inner. So, the RANK value does not matter.

-   Cache = no for right table
-   Cache = no when left table is DB, Cache = yes when left table is File or Any

Runtime performance option: When the number of rows is smaller in one source than another source, use the smaller sources as the RIGHT \(outer\). This setting improves runtime performance but affects memory. Choose this option when there are few resource-consuming transforms.

When the LEFT table is a database, choose Cache=No. When the LEFT table is a File or Any, choose Cache=Yes.

> ### Note:  
> Index must be defined for join columns on the DB table.



### Cache Size Estimate

When any input source is cached for join, the amount cache memory used by the Flowagent engine is roughly estimated using the formula.

> ### Note:  
> Cache size in bytes = Number of rows \* Number of columns \* 20 bytes \(average column size\) \* 1.3 \(30% overhead\).

Number columns refer to the number of columns selected in the JOIN from the table plus the number of join columns.



<a name="loioa415f61f6fc54043847dd3800018bf61__section_knq_5f3_vdb"/>

## Input

None



<a name="loioa415f61f6fc54043847dd3800018bf61__section_swc_cg3_vdb"/>

## Output

None

> ### Restriction:  
> The Data Transform operator does not work if it is connected to another Data Transform operator.

