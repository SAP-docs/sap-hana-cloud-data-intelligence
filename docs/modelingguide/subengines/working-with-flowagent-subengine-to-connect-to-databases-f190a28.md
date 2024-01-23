<!-- loiof190a28f26b344828fddead0d5faab94 -->

# Working with Flowagent Subengine to Connect to Databases

Partitioning the source data allows us to load data in chunks there by overcome memory pressure and by doing it in parallel we can load data faster and improve overall performance.



## Partitioning

Below are supported partitioning methods with the [Connectivity (via Flowagent)](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/4055624226f14da5923278c36ec23a0e.html "") :arrow_upper_right: operators.



### Logical Partition

Logical Partitions are user-defined partitions on how to read data from source. For Table Consumer, the user can choose the partition type then add the partition specification as described below.

-   `defaultPartition`: The partition which fetches all rows that are not filtered by the other partitions \(you can disable it by setting defaultPartition to false\);

-   `conditions`: Each condition represents a set of filters that are performed on a certain column;

    -   `columnExpression`: The column where the filters are applied. It can be either the column name or a function on it \(for example: `TRUNC(EMPLOYEE_NAME)`\);

    -   `type`: The filter type. It can be either "LIST" \(to filter exact values\) or "RANGE" \(to filter a range of values\);

    -   `dataType`: The data type of the elements. It can be either "STRING", "NUMBER" or "EXPRESSION";

    -   `elements`: Each element represents a different filter, and its semantics depends on the "type" \(see above\).


-   When more than one condition is presented, a cartesian product performed among the elements of each condition. For example:

    -   Condition A: \[C1, C2\]

    -   Condition B: \[C3, C4\]

    -   Resulting filters: \[\(C1, C3\), \(C1, C4\), \(C2, C3\), \(C2, C4\)\]



Ex: Let's assume we have a source table called EMPLOYEE that has the following schema:

```
CREATE TABLE EMPLOYEE(
    EMPLOYEE_ID NUMBER(5) PRIMARY KEY,
    EMPLOYEE_NAME VARCHAR(32),
    EMPLOYEE_ADMISSION_DATE DATE
);
```

**RANGE**

A JSON representing a RANGE partition is shown below, where the elements represent ranges. Thus, they need to be sorted in ascending order.

**Numeric Partitions**

```
{
  "defaultPartition": true,
  "conditions": [
    {
      "columnExpression": "EMPLOYEE_ID",
      "type": "RANGE",
      "dataType": "NUMBER",
      "elements": [
        "10",
        "20",
        "30"
      ]
    }
  ]
}
```

**String Partitions**

```
{
  "defaultPartition": true,
  "conditions": [
    {
      "columnExpression": "EMPLOYEE_NAME",
      "type": "RANGE",
      "dataType": "STRING",
      "elements": [
        "M",
        "T"
      ]
    }
  ]
}
```

**Expression Partitions**

```
{
  "defaultPartition": true, 
  "conditions": [
    {
      "columnExpression": "EMPLOYEE_ADMISSION_DATE",
      "type": "RANGE",
      "dataType": "EXPRESSION",
      "elements": [
        "TO_DATE('2012-01-01', 'YYYY-MM-DD')",
        "TO_DATE('2015-01-01', 'YYYY-MM-DD')"
      ]
    }
  ]
}
```

**LIST**

List partitions can be used to filter exact values. Each element represents a different filter.

**Numeric partitions**

```
{
  "defaultPartition": true, 
  "conditions": [
    {
      "columnExpression": "EMPLOYEE_ID",
      "type": "LIST",
      "dataType": "NUMBER",
      "elements": [
        "10",
        "20",
        "50"
      ]
    }
  ]
}
```

**String partitions**

```
{
  "defaultPartition": false,
  "conditions": [
    {
      "columnExpression": "EMPLOYEE_NAME",
      "type": "LIST",
      "dataType": "STRING",
      "elements": [
        "Jhon",
        "Ana",
        "Beatrice"
      ]
    }
  ]
}
```

**Expression partitions**

```
{
  "defaultPartition": false,
  "conditions": [
    {
      "columnExpression": "TRUNC(EMPLOYEE_ADMISSION_DATE)",
      "type": "LIST",
      "dataType": "EXPRESSION",
      "elements": [
        "TO_DATE('2012-07-17', 'YYYY-MM-DD')"
      ]
    }
  ]
}
```

**COMBINED**

```
{
  "defaultPartition": true, 
  "conditions": [
    {
      "columnExpression": "EMPLOYEE_NAME",
      "type": "LIST",
      "dataType": "NUMBER",
      "elements": [
        "Beatrice",
        "Ana"
      ]
    },
    {
      "columnExpression": "EMPLOYEE_ADMISSION_DATE",
      "type": "RANGE",
      "dataType": "EXPRESSION",
      "elements": [
        "TO_DATE('2015-01-01', 'YYYY-MM-DD')",
        "TO_DATE('2016-01-01', 'YYYY-MM-DD')"
      ]
    }
  ]
}
```

> ### Note:  
> -   Operator auto-generates the default partition, so you don't have to define it. It can be disabled by setting the property `"defaultPartition": false`.
> 
> -   For range partition the default partition is greater than last element. So ensure that the elements are ordered in ascending order.



### Physical Partition

> ### Note:  
> Applicable to [Oracle Table Consumer (Deprecated)](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/42350ab198a649fdb047d6f2bdbbd072.html "The Oracle Table Consumer reads from an Oracle table or view.") :arrow_upper_right: only.

Physical partitions are partitions defined directly on the source, using Oracle partitioning concept.

Limitations:

-   Hash partitioning is not supported.

-   Sub-partitioning is not supported.




### Row ID Partition

> ### Note:  
> Applicable to [Oracle Table Consumer (Deprecated)](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/42350ab198a649fdb047d6f2bdbbd072.html "The Oracle Table Consumer reads from an Oracle table or view.") :arrow_upper_right: only.

Row ID partitions are partitions generated automatically based on the row id of the columns. You must supply the number of partitions, and the range of row id partitions is generated automatically based on it.



### Parallel Load With Partitioning

When an operator has partitions, it sends SQL statements in the output port equal to the number of partitions \(including the default partition\), each SQL with a WHERE condition equivalent to the partition. In order to enable parallel load of partitions, it is necessary to put the next Flowagent producer in the pipeline inside a group with multiplicity higher than one, preferentially with multiplicity equal to the number of partitions to enable parallel load of all partitions at the same time.

Note that each producer inside the group generates an output. If you want to prevent the next operator after the producer to be triggered before all partitions are finished \(example: Graph Terminator\), connect the producer to a Constant Generator with `counter` equal to the number of partitions.



### Partition Recovery

Currently there are none automatic recovery mechanism in place. In case any partition fail during the load, the graph stops \(unless the error port of the producer is mapped\).

Consider the following for partition recovery:

-   Retrigger the graph again with table producer mode set to truncate or overwrite;

-   Use a Javascript operator to retrigger only the failed partitions \(see the sample graph provided here\).


