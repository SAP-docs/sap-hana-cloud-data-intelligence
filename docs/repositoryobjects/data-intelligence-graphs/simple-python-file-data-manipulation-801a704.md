<!-- loio801a70440b204ba89034ea2b931064ea -->

# Simple Python File Data Manipulation

Exemplifies file data manipulation using plain Python with only built-in modules and writing the manipulated data back to another file.



<a name="loio801a70440b204ba89034ea2b931064ea__section_zmq_1vc_1kb"/>

## Prerequisites

For this graph, you wil need:

-   a file containing data.

    In the preconfigured example a CSV format file ``test_input.csv`` is assumed to sit in the ``/files/exampleData/scenarioTemplates`` folder. It should have a header row including an \`id\` column, use "," \(comma\) as column separator and contain numerical data \(except for the \`id\` column, which may be string type\).




<a name="loio801a70440b204ba89034ea2b931064ea__section_og5_sb2_1kb"/>

## Configure and Run

1.  Choose Run As from the Run drop-down menu and select the "default" configuration substitutions to run the graph with a preconfigured example configuration.

2.  Click on the Script button of the Process Data operator and enter the Python code that performs the data manipulation. Consult the operator documentation for details.

    The preconfigured example script will insert an additional row of data between each data row in the test\_input.csv file that contains interpolated values for each numerical column.

3.  Enter the path of the file containing the input data in the Path configuration parameter of the Read Input File operator.

    The example configuration includes ``/exampleData/scenarioTemplates/test_input.csv`` for this parameter \(it will prepend the ``/files`` prefix, matching the folder found in System Management\).

4.  Enter the file path for the data manipulation result in the Path configuration parameter of the Write Results File operator.

    In the preconfigured example the results will be written to a file ``test_result_py.csv`` in the ``/files/exampleData/scenarioTemplates`` folder.

5.  Run the graph by clicking the Run button.


