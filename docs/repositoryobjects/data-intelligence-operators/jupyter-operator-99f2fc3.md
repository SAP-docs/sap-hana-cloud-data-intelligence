<!-- loio99f2fc3c4e7342998a00527320f100c0 -->

# Jupyter Operator

The Jupyter operator launches a Jupyter notebook application where you create notebooks to interact with the data flow using Python code.

The Jupyter operator runs on Python 3.9, and therefore, behaves like the [Python3 Operator](python3-operator-0211803.md).

The Jupyter operator offers two run modes:

-   **Interactive mode:** you interact with the data stream by accessing the Jupyter notebook user interface. After you've created the applicable behavior for your script, switch to productive mode.
-   **Productive mode:** the Jupyter operator behaves like the Python 3 operator, which doesn't require user interaction to run the cells.

Because of the Modeler's asynchronous nature, it processes data with callbacks as in the following example:

> ### Example:  
> To have the Modeler run the callback when the in port receives new data, set the callback `set_port_callback("in", callback_name)`.



<a name="loio99f2fc3c4e7342998a00527320f100c0__section_dyd_cd1_1zb"/>

## Configuration Parameters

Configure the Jupyter operator using the parameters specific to the operator, including the notebook location and the mode of execution. The following table contains descriptions for the Jupyter operator configuration parameters.


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Description

</th>
<th valign="top">

Values

</th>
</tr>
<tr>
<td valign="top">

Notebook File Path

</td>
<td valign="top">

**Required.** Path to the notebook to be created or to be opened from the file system or Machine Learning \(ML\) scenario.

> ### Note:  
> Save new notebooks to the graph folder only; include only the file name in the file path.

For notebooks that belong to an ML scenario, place the Jupyter operator in a graph created from the ML Scenario Manager. Use a path that includes the file name of the notebook.

To reference an existing file path, use the absolute path from the file system. When you use an existing file path, it is a path from vrep that starts with "/files".

If the referenced file doesn't exist, the graph fails.

</td>
<td valign="top">

-   **ID:** notebookFilePath
-   **Type:** string
-   **Default:** “”



</td>
</tr>
<tr>
<td valign="top">

Productive

</td>
<td valign="top">

**Required.** Specify whether the operator runs in productive mode.

</td>
<td valign="top">

-   **ID:** productive
-   **Type:** boolean
-   **Default:** false

Productive

</td>
</tr>
<tr>
<td valign="top">

Timeout

</td>
<td valign="top">

**Required.** The maximum number of seconds to wait for data at an input port.

</td>
<td valign="top">

-   **ID:** timeout
-   **Type:** integer
-   **Default:** 5



</td>
</tr>
</table>



<a name="loio99f2fc3c4e7342998a00527320f100c0__section_pln_gd1_1zb"/>

## Input

None.



<a name="loio99f2fc3c4e7342998a00527320f100c0__section_dgw_gd1_1zb"/>

## Output

None.

-   **[Opening the Jupyter Notebook](opening-the-jupyter-notebook-fce511c.md "Open the Jupyter notebook user interfaceIn interactive mode, and run the cells to interact with the data stream.")**  
Open the Jupyter notebook user interfaceIn interactive mode, and run the cells to interact with the data stream.
-   **[Jupyter Operator Examples](jupyter-operator-examples-6f49ea7.md "Use the examples in this topic to help you understand how to work with the Jupyter operator and notebook.")**  
Use the examples in this topic to help you understand how to work with the Jupyter operator and notebook.
-   **[Jupyter Operator Predefined Functions](jupyter-operator-predefined-functions-4fd1229.md "There are functions available from the Jupyter notebook that you can use in SAP Data Intelligence and the Jupyter operator.")**  
There are functions available from the Jupyter notebook that you can use in SAP Data Intelligence and the Jupyter operator.
-   **[Correspondence Between Modeler and Python Data Types](correspondence-between-modeler-and-python-data-types-81f40a2.md "The SAP Data Intelligence Modeler data types are types that are allowed in the operator ports. The Modeler translates Phthon3 data types
		to supported data types. ")**  
The SAP Data Intelligence Modeler data types are types that are allowed in the operator ports. The Modeler translates Phthon3 data types to supported data types.

