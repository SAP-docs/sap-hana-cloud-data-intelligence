<!-- loio9f64ea7308f64cdfb5c9b51560350818 -->

# Creating Categories

Create a custom category for the operators or graphs that you create.



## Procedure

1.  Open the Repository tab in the navigation pane at left.

2.  Expand the folder named “general” and then expand the subfolder named “ui”.

3.  Double-click `settings.json`.

    The JSON file opens in the main pane.

4.  Add the category information to the array of categories listed.

    The category name follows the same operator title naming constraints.

    > ### Example:  
    > ```
    > {
    >     "name": "Category Name",
    >     "entities": [
    >         "com.sap.foo.bar",
    >         "com.sap.operator.test"
    > ```


