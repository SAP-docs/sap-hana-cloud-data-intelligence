<!-- loio740d7610fc24432da61a50734c18bee8 -->

# Simple Javascript File-to-DB Data Manipulation

File data manipulation using plain Javascript \(without any libraries\) and writing the manipulated data to an SAP HANA database table.



<a name="loio740d7610fc24432da61a50734c18bee8__section_gdy_mrx_zkb"/>

## Prerequisites

For this graph, you wil need:

-   a connection to an SAP HANA database.

-   a file containing data.




<a name="loio740d7610fc24432da61a50734c18bee8__section_n2y_vyw_zkb"/>

## Configure and Run

1.  Click on the Script button of the **Process Data** operator and enter the Javascript code that performs the data manipulation. Consult the operator documentation for details. Please note that the operator supports ECMAScript 2009 \(ES5\) specifications.

2.  Enter the path of the file containing the input data in the Path configuration parameter of the **Read Input File** operator.

3.  Configure the database connection and the target table for the data manipulation result in the *Connection*, *Table Name*, and *Table Columns* configuration parameters of the **Write to HANA DB** operator.

4.  Run the resulting graph by clicking the *Run* button.

