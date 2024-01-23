<!-- loio29d8196f8ccd4e0c997960a709176fc7 -->

# Simple Javascript File Data Manipulation

Exemplifies file data manipulation using plain Javascript \(without any libraries\) and writing the manipulated data back to another file.



<a name="loio29d8196f8ccd4e0c997960a709176fc7__section_zmq_1vc_1kb"/>

## Prerequisites

For this graph, you wil need:

-   a file containing data.

    In the preconfigured example a JSON format file ``test_input.json`` is assumed to sit in the ``/files/exampleData/scenarioTemplates`` folder. It should contain an array of objects with a string type \`id\` property and some numerical data properties.




<a name="loio29d8196f8ccd4e0c997960a709176fc7__section_og5_sb2_1kb"/>

## Configure and Run

1.  Choose Run As from the Run drop-down menu and select the "default" configuration substitutions to run the graph with a preconfigured example configuration.

2.  Click on the Script button of the Process Data operator and enter the Javascript code that performs the data manipulation. Consult the operator documentation for details. Please note that the operator supports ECMAScript 2009 \(ES5\) specifications.

    The preconfigured example script will insert an additional row of data between each data row in the test\_input.json file that contains interpolated values for each numerical column.

3.  Enter the path of the file containing the input data in the Path configuration parameter of the Read Input File operator.

    The example configuration includes ``/exampleData/scenarioTemplates/test_input.json`` for this parameter \(the operator will prepend the ``/files/`` prefix, matching the folder found in System Management\).

4.  Enter the file path for the data manipulation result in the Path configuration parameter of the Write Results File operator.

    In the preconfigured example the results will be written to a file test\_result\_js.json in the files/exampleData/scenarioTemplates folder.

5.  Run the graph by clicking the Run button.


