<!-- loio7df99cc10bd9481fa806671afadd4d85 -->

# Add a Filter

For a given task, you can optionally add one or more filters to a dataset to customize the target.



## Procedure

1.  In the *Tasks* list, browse to the replication flow to configure.

2.  For the dataset to filter, in the *Source Filter* column, choose the *Filter* icon.

3.  In the *Provide Filter Values - *<dataset\_name\>** dialog, choose a column to filter.

4.  Under *Define values for *<column\_name\>**, choose an operator from the dropdown list and add a value in the field.

5.  To add more filters for this or other columns, click the + button to add another row.

    -   More than one filter on different columns applies the AND operator.
    -   More than one filter on the same column applies the OR operator.

    For example, filtering a dataset on the product ID number 123 for the countries United States and Germany results in the following:

    \(PRODUCT\_ID = 123\) AND \(COUNTRY = 'US' OR COUNTRY = 'DE'\)

    Columns that have filters applied are marked. You can display only the columns that have filters applied by choosing the checkbox above the list.

6.  Choose *OK*.




<a name="loio7df99cc10bd9481fa806671afadd4d85__result_e54_xkg_hqb"/>

## Results

The dataset's *Source Filter* column now displays *Filtered*. Hover over the word *Filtered* to view the columns that have filters applied.

