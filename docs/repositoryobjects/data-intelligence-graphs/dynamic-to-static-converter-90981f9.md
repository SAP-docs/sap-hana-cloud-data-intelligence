<!-- loio90981f90ede648438685bfcf3831f178 -->

# Dynamic to Static Converter

This scenario showcases how to read data from an input with dynamic data type and write into an output with static data type using a Python Operator.



Python Generator generates an example table and sends it as data into the output.

Python Converter will read the input that is receiving a table into a callback method. This method defines a size to each set of data that is sent on the output via a stream. It sends the data in batches until no more data are available on the input.

The Terminal shows all data sent from the Python Operator.



<a name="loio90981f90ede648438685bfcf3831f178__section_akz_jpl_qrb"/>

## Create and Update Static Types

To use a different static data type in the Python Converter output, you can create a custom type by following the steps below:

1.  Access the graph configuration and open the data types tab.

2.  Create or edit the data types.

3.  You will need to define ID, type, description, and properties to your data type.

4.  Save the data settings.

5.  Access the port configuration to change the data type ID. The custom data type and port must be the same type \(structure, table, or scalar\).




<a name="loio90981f90ede648438685bfcf3831f178__section_uld_rpl_qrb"/>

## See the Code for Python Operator

If you would like to see the code used for the operations, use the context menu "Open Script" of the Python Operator.

