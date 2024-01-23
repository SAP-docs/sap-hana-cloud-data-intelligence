<!-- loiobbba1bed23d44484a06f3f378b4905f6 -->

# Consuming Excel Files with Structured File Consumer Operator

Use a structured file consumer operator and select an Excel file as a source in a pipeline to transform the Excel format to a table or dataset.



## Context

After you open the structured file consumer operator in your graph, select a connection in *Connection ID* and an Excel file source in *Source*. Then perform the following steps to configure the Excel worksheet:



## Procedure

1.  Select *Data Preview*.

    The *Excel Properties* pane opens. The Modeler fetches the first sheet in the selected Excel file.

    The lower portion of the Excel Properties pane shows the source columns in the table that also includes the qualified names and the data types. You can change the data types, if necessary.

2.  **Optional:** Select *Modify* to select a different worksheet. The *Excel Properties* dialog opens.

    1.  Select a sheet number from the *Select Sheet* list.

    2.  Select *Set first row as header* to use the first row of the sheet as the header row in the resulting table.

    3.  Select *OK*.





<a name="loiobbba1bed23d44484a06f3f378b4905f6__result_cdq_slt_jvb"/>

## Results

The Modeler doesn't transform formulas into the final table or dataset. Therefore, if your Excel sheet contains cells with formulas, the result is an empty cell in the final table or dataset.

