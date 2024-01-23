<!-- loio83ccb1ce7fd94803acd623d9303c6caf -->

# Logical Partitions

Logical partitions are user-defined chunks of data, where each chunk contains a filter that specifies the chunk of data to be read.

These chunks are loaded in parallel so that the full load can be done in a shorter amount of time.

For Table Consumers, a simple filter is automatically added and no extra work is required.

For SQL Consumers, we modify the SQL injecting a `WHERE` condition. If additional conditions are required in the SQL statement, a placeholder called`$partition_specification` can be provided in the native SQL statement itself, which is replaced by the `WHERE` condition. For example, here is a native SQL statement:

> ### Sample Code:  
> ```
> SELECT * FROM EMPLOYEE $partition_specification LIMIT 10;
> ```

The placeholder in the native SQL statement is replaced with the following `WHERE` condition:

> ### Sample Code:  
> ```
> SELECT * FROM EMPLOYEE WHERE ... LIMIT 10;
> ```



<a name="loio83ccb1ce7fd94803acd623d9303c6caf__section_k5b_nsz_2pb"/>

## Partition Definitions

-   Conditions represent a set of filters that are performed on a certain column.


    <table>
    <tr>
    <td valign="top">
    
    columnExpression
    
    </td>
    <td valign="top">
    
    The column where the filters are applied. The filter can be on a column name or a function \(for example, TRUNC\(EMPLOYEE\_NAME\)\);
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    type
    
    </td>
    <td valign="top">
    
    The filter type. It can be either “LIST” \(to filter exact values\) or “RANGE” \(to filter a range of values\);
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    dataType
    
    </td>
    <td valign="top">
    
    The data type of the elements. It can be either “STRING”, “NUMBER” or “EXPRESSION”;
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    elements
    
    </td>
    <td valign="top">
    
    Each element represents a different filter, and its semantics depends on the “type” \(see above\).
    
    </td>
    </tr>
    </table>
    
-   When more than one condition is presented, it performs a cartesian product among the elements of each condition, for example:
    -   Condition A: \[C1, C2\]
    -   Condition B: \[C3, C4\]
    -   Resulting filters: \[\(C1, C3\), \(C1, C4\), \(C2, C3\), \(C2, C4\)\]

-   defaultPartition is the condition that filters all rows that were not filtered by any other partition \(enabled by default\).

Below it is shown some examples of different types of partitions. For the examples, let’s assume we have a source table called EMPLOYEE that has the following schema:

> ### Sample Code:  
> ```
> CREATE TABLE EMPLOYEE(
>     EMPLOYEE_ID NUMBER(5) PRIMARY KEY,
>     EMPLOYEE_NAME VARCHAR(32),
>     EMPLOYEE_ADMISSION_DATE DATE
> );
> ```

In SQL Consumer, we use the following SQL statement:

> ### Sample Code:  
> ```
> SELECT * FROM EMPLOYEEE $partition_specification
> ```

In Table Consumer, we select the EMPLOYEEE table.



<a name="loio83ccb1ce7fd94803acd623d9303c6caf__section_v4r_ttz_2pb"/>

## Range Partitions

A JSON representing a RANGE partition is shown below, where the elements represent ranges, thus, they need to be sorted in ascending order.

The default partition filters the values higher or equal to the last defined interval. Additionally, the filters include any null values in the column.



### Range Numeric Partitions

> ### Sample Code:  
> ```
> {
>   "defaultPartition": true,
>   "conditions": [
>     {
>       "columnExpression": "EMPLOYEE_ID",
>       "type": "RANGE",
>       "dataType": "NUMBER",
>       "elements": [
>         "10",
>         "20",
>         "30"
>       ]
>     }
>   ]
> }
> ```

This generates the following SQL statements:

> ### Sample Code:  
> ```
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ID < 10
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ID >= 10 AND EMPLOYEE_ID < 20
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ID >= 20 AND EMPLOYEE_ID < 30
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ID >= 30 OR EMPLOYEE_ID IS NULL
> ```



### Range String Partitions

> ### Sample Code:  
> ```
> {
>   "defaultPartition": true,
>   "conditions": [
>     {
>       "columnExpression": "EMPLOYEE_NAME",
>       "type": "RANGE",
>       "dataType": "STRING",
>       "elements": [
>         "M",
>         "T"
>       ]
>     }
>   ]
> }
> ```

This generates the following SQL statements:

> ### Sample Code:  
> ```
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_NAME < 'M'
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_NAME >= 'M' AND EMPLOYEE_NAME < 'T'
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_NAME >= 'T' OR EMPLOYEE_NAME IS NULL
> ```



### Range Expression Partitions

> ### Sample Code:  
> ```
> {
>   "defaultPartition": true, 
>   "conditions": [
>     {
>       "columnExpression": "EMPLOYEE_ADMISSION_DATE",
>       "type": "RANGE",
>       "dataType": "EXPRESSION",
>       "elements": [
>         "TO_DATE('2012-01-01', 'YYYY-MM-DD')",
>         "TO_DATE('2015-01-01', 'YYYY-MM-DD')"
>       ]
>     }
>   ]
> }
> ```

This generates the following SQL statements:

> ### Sample Code:  
> ```
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ADMISSION_DATE < TO_DATE('2012-01-01', 'YYYY-MM-DD')
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ADMISSION_DATE >= TO_DATE('2012-01-01', 'YYYY-MM-DD' AND EMPLOYEE_ADMISSION_DATE < TO_DATE('2015-01-01', 'YYYY-MM-DD')
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ADMISSION_DATE >= TO_DATE('2015-01-01', 'YYYY-MM-DD') OR EMPLOYEE_ADMISSION_DATE IS NULL
> ```



<a name="loio83ccb1ce7fd94803acd623d9303c6caf__section_jxg_vc1_fpb"/>

## List Partitions

List partitions can be used to filter exact values. Each element represents a different filter.

The default partition filters values that are different than all listed values.



### List Numeric Partitions

> ### Sample Code:  
> ```
> {
>   "defaultPartition": true, 
>   "conditions": [    {
>       "columnExpression": "EMPLOYEE_ID",
>       "type": "LIST",
>       "dataType": "NUMBER",
>       "elements": [
>         "10",
>         "20",
>         "50"
>       ]
>     }
>   ]
> }
> ```

This generates the following SQL statements:

> ### Sample Code:  
> ```
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ID = 10
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ID = 20
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ID = 50
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_ID != 10 AND EMPLOYEE_ID != 20 AND EMPLOYEE_ID != 50 OR EMPLOYEE_ID IS NULL
> ```



### List String Partitions

> ### Sample Code:  
> ```
> {
>   "defaultPartition": false,
>   "conditions": [
>     {
>       "columnExpression": "EMPLOYEE_NAME",
>       "type": "LIST",
>       "dataType": "STRING",
>       "elements": [
>         "Jhon",
>         "Ana",
>         "Beatrice"
>       ]
>     }
>   ]
> }
> ```

This generates the following SQL statements:

> ### Sample Code:  
> ```
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_NAME = 'Jhon'
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_NAME = 'Ana'
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_NAME = 'Beatrice'
> ```

Notice that the default partition was disabled.



### List Expression Partitions

> ### Sample Code:  
> ```
> {
>   "defaultPartition": false,
>   "conditions": [
>     {
>       "columnExpression": "TRUNC(EMPLOYEE_ADMISSION_DATE)",
>       "type": "LIST",
>       "dataType": "EXPRESSION",
>       "elements": [
>         "TO_DATE('2012-07-17', 'YYYY-MM-DD')"
>       ]
>     }
>   ]
> }
> ```

This generates the following SQL statements:

> ### Sample Code:  
> ```
> SELECT * FROM EMPLOYEE WHERE TRUNC(EMPLOYEE_ADMISSION_DATE) = TO_DATE('2012-07-17', 'YYYY-MM-DD')
> ```



<a name="loio83ccb1ce7fd94803acd623d9303c6caf__section_ehb_yc1_fpb"/>

## Combined Partitions

Combine both, list and range partitions. The default partition filters all values that are higher or equal than the last interval defined in the range partition.

> ### Sample Code:  
> ```
> {
>   "defaultPartition": true, 
>   "conditions": [
>     {
>       "columnExpression": "EMPLOYEE_NAME",
>       "type": "LIST",
>       "dataType": "NUMBER",
>       "elements": [
>         "Beatrice",
>         "Ana"
>       ]
>     },
>     {
>       "columnExpression": "EMPLOYEE_ADMISSION_DATE",
>       "type": "RANGE",
>       "dataType": "EXPRESSION",
>       "elements": [
>         "TO_DATE('2015-01-01', 'YYYY-MM-DD')",
>         "TO_DATE('2016-01-01', 'YYYY-MM-DD')"
>       ]
>     }
>   ]
> }
> ```

This generates the following SQL statements:

> ### Sample Code:  
> ```
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_NAME = 'Beatrice' AND EMPLOYEE_ADMISSION_DATE < TO_DATE('2015-01-01', 'YYYY-MM-DD')
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_NAME = 'Beatrice' AND EMPLOYEE_ADMISSION_DATE >= TO_DATE('2015-01-01', 'YYYY-MM-DD') AND EMPLOYEE_ADMISSION_DATE < TO_DATE('2016-01-01', 'YYYY-MM-DD')
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_NAME = 'Ana' AND EMPLOYEE_ADMISSION_DATE < TO_DATE('2015-01-01', 'YYYY-MM-DD')
> SELECT * FROM EMPLOYEE WHERE EMPLOYEE_NAME = 'Ana' AND EMPLOYEE_ADMISSION_DATE >= TO_DATE('2015-01-01', 'YYYY-MM-DD') AND EMPLOYEE_ADMISSION_DATE < TO_DATE('2016-01-01', 'YYYY-MM-DD')
> SELECT * FROM EMPLOYEE WHERE (EMPLOYEE_ADMISSION_DATE >= TO_DATE('2016-01-01', 'YYYY-MM-DD') OR EMPLOYEE_ADMISSION_DATE IS NULL) OR (EMPLOYEE_NAME != 'Beatrice' AND EMPLOYEE_NAME != 'Ana' OR EMPLOYEE_NAME IS NULL)
> ```

> ### Note:  
> -   Operator auto-generates the default partition, so the user does not need to define it, but it can be disabled by setting the property “defaultPartition”: false.
> -   For range partition the default partition is greater than last element. So, ensure that the elements are ordered in ascending order.
> -   If some element calls a built-in function, the user must set the datatype to EXPRESSION.



<a name="loio83ccb1ce7fd94803acd623d9303c6caf__section_j2g_421_fpb"/>

## Physical Partitions

Physical partitions are partitions that are defined directly on the source, using Oracle partitioning concept. Limitations include:

-   Hash partitioning is not supported.
-   Subpartitioning is not supported.

> ### Note:  
> Only Oracle connection types support this type of partition.



<a name="loio83ccb1ce7fd94803acd623d9303c6caf__section_wz5_t21_fpb"/>

## Row ID Partitions

Row ID partitions are partitions that are generated automatically based on the row id of the columns. The user must supply the number of partitions, and the range of row ID partitions are generated automatically based on it.

> ### Note:  
> Only Oracle connection types support this type of partition.



<a name="loio83ccb1ce7fd94803acd623d9303c6caf__section_zpn_w21_fpb"/>

## Parallel Load with Partitioning

The benefit of using partitioning is to ingest data in parallel, loading multiple partitions at the same time. To load multiple partitions, we use the group concept of Pipeline Modeler, where we place some operators inside a group and multiple instances are created.

The number of instances created is defined by the multiplicity set in the group. It is recommended to set the multiplicity with the same size as the number of partitions so that each instance processes exactly one partition. However, if there are more partitions than instances, as soon as one instance is done, it picks up a new partition to run.

Note that each producer generates an output. If you want to prevent the next operator after the producer to be triggered before all partitions have finished \(example: Graph Terminator\), connect the producer to a Constant Generator with counter equal to the number of partitions. Alternatively, you can use the message headers in the operators to know when all partitions have finished. For details, see [Partitioning](partitioning-86085d9.md).

> ### Note:  
> SAP IQ does not support writing data in parallel, so the group multiplicity has to be set to 1.



<a name="loio83ccb1ce7fd94803acd623d9303c6caf__section_nht_cf1_fpb"/>

## Operator Grouping

There are two different operator categories that support grouping: Connectivity \(via Flowagent\) and Structured Data Operators. Each category has a different grouping strategy, and it is described below.



### Connectivity \(via Flowagent\)

In the operators from the Connectivity \(via Flowagent\) category, the only operator placed in a group is the producer. You can see in the example below how it is done.

> ### Sample Code:  
> ```
> 
>                    +------------------+
>   +-----------+    |  +------------+  |
>   | consumer1 | -> |  | producer1  |  |
>   +-----------+    |  +------------+  |
>                    |           group1 |
>                    +------------------+
> ```

This example can be seen in the com.sap.dh.ingestion.sqlconsumer sample graph.



### Structured Data Operators

When using the operators from the Structured Data Operators category, there is a different grouping strategy. There, both consumer and producer must be placed inside the group as show in the example below.

> ### Sample Code:  
> ```
>   
>   +-----------------------------------+
>   | +-----------+     +------------+  |
>   | | consumer1 | ->  | producer1  |  |
>   | +-----------+     +------------+  |
>   |                            group1 |
>   +-----------------------------------+
> ```

This example can be seen in the com.sap.scenarioTemplates.ETLFromDB.cdcInitialLoad sample graph.

