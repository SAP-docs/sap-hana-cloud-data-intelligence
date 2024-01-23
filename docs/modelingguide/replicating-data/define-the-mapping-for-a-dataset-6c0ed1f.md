<!-- loio6c0ed1f272c24d2c81b6186705eafcdc -->

# Define the Mapping for a Dataset

For existing target tables, you can edit the mapping of a dataset to customize it. Or, for a target table that doesn't exist yet, SAP Data Intelligence replication flow lets you define the table by specifying column names and data-type information.



<a name="loio6c0ed1f272c24d2c81b6186705eafcdc__context_jqs_kb5_xqb"/>

## Context

By default, SAP Data Intelligence replication flow copies all columns from the source dataset to the target dataset. Custom mappings let you add, edit, or remove columns.



## Procedure

1.  View the *Tasks* list.

2.  In the *Mapping* column, choose the *Mapping* icon.

    The *Target Mapping - *<dataset\_name\>** appears.

3.  To filter the list of columns, add a value in the *Search* field.

4.  The following table contains information about the various tasks, such as editing or defining the mapping of a target column.


    <table>
    <tr>
    <th valign="top">

    Task
    
    </th>
    <th valign="top">

    Action
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    **Change the source mapping column**
    
    </td>
    <td valign="top">
    
    Choose a different column from the *Source Mapping* list.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Add a custom mapping expression**
    
    </td>
    <td valign="top">
    
    Enable the *Expression* field and add one or more values. For example:

    -   String constant \(must be surrounded by single quotes\).
    -   Numeric constant such as -123, 123, 123.45.

    You can also use the following supported functions:

    -   CURRENT\_UTCDATE
    -   CURRENT\_UTCTIME
    -   CURRENT\_UTCTIMESTAMP


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Change \(promote\) the data type of a column**
    
    </td>
    <td valign="top">
    
    Enabled only if the target doesn't exist yet.

    SAP Data Intelligence replication flow maps the target data type from the source data type in the mapping editor automatically, ensuring the data type doesn't change. Either maintain the same data type as the source data type, or choose a compatible data type from the list.

    > ### Note:  
    > The list contains all data types regardless of what's compatible to the source data type.

    For information about compatible data types, see [Data Type Compatibility](data-type-compatibility-e81bd11.md).

    > ### Example:  
    > SAP Data Intelligence maps a source data type of int8 to a target data type of int8 automatically.

    You can promote values, such as field length, decimal, scale, and precision, based on the data type.

    > ### Example:  
    > Promote integer data types. When a source data type is int8, promote the target to either int16, int32 or int64.

    SAP Data Intelligence replication flow supports only implicit data type compatibility.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Identify the column as a primary key**
    
    </td>
    <td valign="top">
    
    Enabled only if the target doesn't exist yet.

    Choose the *Key* checkbox.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Add a column to the target**
    
    </td>
    <td valign="top">
    
    Enabled only if the target doesn't exist yet.

    Choose *Create*. A new row appears at the bottom of the list.

    -   Add the new column name and the desired custom mapping expression.
    -   Alternately, disable the *Expression* field to enable the *Source Mapping* drop-down list and choose a different source column.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Delete a column from the target**
    
    </td>
    <td valign="top">
    
    Enabled only if the target dataset doesn't exist yet.

    Choose the column name and choose *Delete.*
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Reorder the columns**
    
    </td>
    <td valign="top">
    
    Enabled only if the target dataset doesn't exist yet.

    Choose the column row and choose *First*, *Up*, *Down*, or *Last*.
    
    </td>
    </tr>
    </table>
    
5.  Choose *OK* to confirm the mapping changes.




<a name="loio6c0ed1f272c24d2c81b6186705eafcdc__result_gmv_wkg_hqb"/>

## Results

The dataset's *Mapping* column now displays *Transformed*. Hover over the word *Transformed* to view the columns that have transformations applied.

