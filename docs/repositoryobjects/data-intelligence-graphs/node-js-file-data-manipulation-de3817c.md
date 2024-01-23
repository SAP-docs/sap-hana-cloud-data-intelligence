<!-- loiode3817cf734245da90ecfe66c0a767ae -->

# Node.js File Data Manipulation

This graph exemplifies file data manipulation using Node.js and writing the manipulated data back to another file.



## Prerequisites

For this graph to run you will need:

-   a file containing data.

    In the preconfigured example a CSV format file ``test_large.csv`` is assumed to sit in the ``/files/exampleData/scenarioTemplates`` folder.




<a name="loiode3817cf734245da90ecfe66c0a767ae__section_eqn_vk2_vkb"/>

## Configure and Run the Graph

1.  To modify the data manipulation performed by the custom operator go to the *Operators* tab and find the *Process Data with Node.js* operator, then select *Edit* from the operator's context menu. Note that the operator supports ECMAScript 2015 \(ES6\) specifications.

2.  Enter the path of the file containing the input data in the *Path* configuration parameter of the Read Input File operator.

    The example configuration includes ``/exampleData/scenarioTemplates/test_input.json`` for this parameter \(the operator will prepend the ``/files/``, matching the folder found in System Management\).

3.  Enter the file path for the data manipulation result in the *Path* configuration parameter of the Write Results File operator.

    In the preconfigured example the results will be written to a file ``test_custom_node.csv`` in the ``/files/exampleData/scenarioTemplates`` folder.

4.  Run the graph by clicking the *Run* button.

