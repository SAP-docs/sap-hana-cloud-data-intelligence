<!-- loio0daa1213068847d58eac9bc6fc09d5ff -->

# Normal Usage

If you want to create simple scripts quickly, we recommend that you customize the behavior of operators using the SAP Data Intelligence Modeler user interface.



There are two ways to customize the behavior of a *Python3 Operator*:

-   Drag the *Python3 Operator* to the graph canvas and edit the script of the operator by right-clicking on it and clicking the open script option.
-   Create a new operator in the *Repository* tab and select *Python3 Operator* as the base operator to be extended.

The advantage of the second approach is that you can reuse your new operator across many graphs, while in the first approach, the edited script is specific to the given graph and operator instance.

To create a new operator in the *Repository* tab using the *Python3 Operator*:

1.  Open the *Repository* tab and expand the *Operators* section.
2.  To create an operator, right-click the appropriate *Operators* subfolder, and select *Create Operator*.
3.  In the dialog, enter the operator name, display name, and base operator and choose *Python3 Operator* as the base operator.
4.  In the operator editor view, you can create input ports, output ports, tags, and configuration parameters, and write your script.

-   **[Using Python Libraries](using-python-libraries-781938a.md "To make Python libraries available to your operator, you can add tags to it so that upon
		graph execution, the appropriate docker image can be chosen. ")**  
To make Python libraries available to your operator, you can add tags to it so that upon graph execution, the appropriate docker image can be chosen.

