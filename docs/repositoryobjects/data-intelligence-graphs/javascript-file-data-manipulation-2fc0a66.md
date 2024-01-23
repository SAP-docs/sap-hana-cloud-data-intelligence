<!-- loio2fc0a66f8dea4586abd3e004e3e0b408 -->

# Javascript File Data Manipulation

Exemplifies file data manipulation using a Javascript custom operator and writing the manipulated data back to another file.



<a name="loio2fc0a66f8dea4586abd3e004e3e0b408__section_zmq_1vc_1kb"/>

## Prerequisites

-   A file containing data.

    In the preconfigured example a JSON format file ``test_input.json`` is assumed to sit in the ``/files/exampleData/scenarioTemplates`` folder. It should contain an array of objects with a string type ``id`` property and some numerical data properties.




<a name="loio2fc0a66f8dea4586abd3e004e3e0b408__section_og5_sb2_1kb"/>

## Configure and Run

1.  Choose Run As from the Run drop-down menu and select the "default" configuration substitutions to run the graph with a preconfigured example configuration.

2.  To modify the data manipulation performed by the custom operator go to the Operators tab and find the Process Data with Javascript operator, then select Edit from the operator's context menu. Please note that the operator supports ECMAScript 2009 \(ES5\) specifications.

3.  Enter the path of the file containing the input data in the Path configuration parameter of the Read Input File operator.

    The example configuration includes ``/exampleData/scenarioTemplates/test_input.json`` for this parameter \(the operator will prepend the ``/files/``, matching the folder found in System Management\).

4.  Enter the file path for the data manipulation result in the Path configuration parameter of the Write Results File operator.

    In the preconfigured example the results will be written to a file ``test_custom_js.json`` in the ``/files/exampleData/scenarioTemplates`` folder.

5.  Run the graph by clicking the Run button.


