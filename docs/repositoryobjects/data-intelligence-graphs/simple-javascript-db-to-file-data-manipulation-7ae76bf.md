<!-- loio7ae76bfcceba4fb0af22e991880e3fee -->

# Simple Javascript DB-to-File Data Manipulation

Manipulation of data from an SAP HANA database table using plain Javascript \(ECMAScript 2009 / ES5\) and writing the manipulated data to a file.



## Prerequisites

For this graph, you wil need:

-   a connection to an SAP HANA database.

-   a database table in SAP HANA containing data.




<a name="loio7ae76bfcceba4fb0af22e991880e3fee__section_n2y_vyw_zkb"/>

## Configure and Run

1.  Enter the SQL statement that reads the input data from the SAP HANA database table in the *Content* configuration parameter of the **SQL Statement** operator.
2.  Choose the connection for the input data in the *Connection* configuration parameter of the **Get Data from DB** operator.
3.  Click on the *Script* button of the *Process Data* operator and enter the Javascript code that performs the data manipulation. Check the documentation for details. Please note that the operator supports ECMAScript 2009 \(ES5\) specifications.
4.  Enter the file path for the data manipulation result in the *Path* configuration parameter of the **Write Results File** operator.
5.  Run the resulting graph by clicking the *Run* button.

