<!-- loio93c128e9c35d4d67afcd59b14a5794a4 -->

# Join Design Considerations

You can control memory and CPU usage used to process joins, improve runtime performance of the joins in the graph, and process more joins within a graph effectively with resource limitations.



<a name="loio93c128e9c35d4d67afcd59b14a5794a4__section_fhk_rs3_qnb"/>

## Join Resource and Performance Control Options

When designing joins within a structured data transform operator, use the following options to help control the resources needed:

-   `Rank`: A number whose value determines if a table should be considered inner or outer. If the rank is higher, the table is outer. If the rank is lower, the table is inner.
-   `Cache`: A value of yes or no determines whether a table should be cached or not. A value of automatic means that the engine decides.



<a name="loio93c128e9c35d4d67afcd59b14a5794a4__section_amw_3t3_qnb"/>

## Choosing Rank and Cache Values for Join

-   DB – database source
-   File – cloud file source
-   Any – any output within a data transform operation like projection or join

One source will be referred as left and other one as right.



<a name="loio93c128e9c35d4d67afcd59b14a5794a4__section_ktg_pt3_qnb"/>

## Inner Join

**DB and DB**

-   Use low rank for the large table and high rank for the small table
-   Cache = no, for both sources

Index must be defined for join columns on the DB table.

Runtime performance option: If index is not defined for the inner table, choose Cache = yes. This setting improves runtime performance but affects memory. Choose this option when there are fewer resources consuming transforms.

**File and DB, Any and DB**

-   Use low rank for the DB and high rank for the file
-   Cache = no, for both sources

Index must be defined for join columns on the DB table.

Runtime performance option: When the number of database rows is less than the number of rows in the file, use a lower rank for the file and set Cache = Yes. This setting improves runtime performance but affects memory. Choose this option when there are fewer resources consuming transforms.

**File and File, Any and File, Any and Any**

-   Use low rank for the smaller source
-   Cache = yes for the low rank source

Index must be defined for join columns on the DB table.

Runtime performance option: When the number of rows is fewer in one source than another source, use low rank for the larger source and set Cache = Yes. This setting improves runtime performance but affects memory. Choose this option when there are fewer resources consuming transforms.



<a name="loio93c128e9c35d4d67afcd59b14a5794a4__section_hkm_d53_qnb"/>

## Left Outer Join

In case of Left Outer Joins, the left source is always chosen as outer irrespective of type, and the right source is chosen as inner. The Rank value is not considered.

-   Cache = no, for left table
-   Cache = no, when right table is DB
-   Cache = yes, when right table is File or Any

When the number of rows is fewer in one source than another source, use the smaller source as Left \(outer\). This setting improves runtime performance but affects memory. Choose this option when there are fewer resources consuming transforms.

-   When the Right table is a database, choose Cache = no. When the Right table is a File or Any, choose Cache = yes.

Index must be defined for join columns in the DB table.



<a name="loio93c128e9c35d4d67afcd59b14a5794a4__section_zbl_l53_qnb"/>

## Right Outer Join

In case of Right Outer Join, the right source is always chosen as outer irrespective of type, and the left source is chosen as inner. The Rank value is not considered.

-   Cache = no, for right table
-   Cache = no, when left table is DB
-   Cache = yes, when left table is File or Any

Runtime performance option: When the number of rows is smaller in one source than another source, use the smaller sources as the RIGHT \(outer\). This setting improves runtime performance but affects memory. Choose this option when there are few resource-consuming transforms.

-   When the LEFT table is a database, choose Cache = no. When the LEFT table is a File or Any, choose Cache = yes.

Index must be defined for join columns on the DB table.



<a name="loio93c128e9c35d4d67afcd59b14a5794a4__section_sgm_553_qnb"/>

## Cache Size Estimate

When any input source is chosen to be cached for join, the amount of cache memory used by the Flowagent engine is roughly estimated using the following formula.

`Cache size in bytes = Number of rows * Number of columns * 20 bytes (average column size) * 1.3 (30% overhead)`

Number of columns here refers to the number of columns selected in the Join from the table plus the number of join columns.

