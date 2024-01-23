<!-- loiobbc1b874df5a483ea359e13a978936d6 -->

# Python File Data Manipulation with Pandas

Exemplifies file data manipulation using Python with the Pandas library and writing the manipulated data back to another file.



<a name="loiobbc1b874df5a483ea359e13a978936d6__section_zmq_1vc_1kb"/>

## Prerequisites

For this graph, you wil need:

-   A file containing data.

    In the preconfigured example a CSV format file ``test_large.csv`` is assumed to sit in the ``/files/exampleData/scenarioTemplates``folder.

    The file should be:

    -   in CSV format including a header row;

    -   structured into four columns t \(representing time\), v \(representing velocity in m/s\), s \(representing distance in m travelled between two data points\), and d \(representing total distance in m travelled since start of the data series\);

    -   sampled at a higher rate than 5 mins.





<a name="loiobbc1b874df5a483ea359e13a978936d6__section_og5_sb2_1kb"/>

## Configure and Run

1.  Choose Run As from the Run drop-down menu and select the "default" configuration substitutions to run the graph with a preconfigured example configuration.

2.  To modify the data manipulation performed by the custom operator go to the Operators tab and find the Process Data with Python operator, then select Edit from the operator's context menu.

3.  Enter the path of the file containing the input data in the Path configuration parameter of the Read Input File operator.

    The example configuration includes ``/exampleData/scenarioTemplates/test_large.csv`` for this parameter \(the operator will prepend the ``/files/`` prefix, matching the folder found in System Management\).

4.  Enter the file path for the data manipulation result in the Path configuration parameter of the Write Results File operator.

    In the preconfigured example the results will be written to a file test\_custom\_py.csv in the files/exampleData/scenarioTemplates folder.

5.  Run the graph by clicking the Run button.


