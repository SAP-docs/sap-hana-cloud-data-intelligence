<!-- loiobba574eb699f4aadb4020d958a3b6ab8 -->

# Multiplexer for Static Outputs

This scenario showcases how to read static data from an input and write to multiple outputs using a Python Operator.



Python Generator generates an example table and sends it as data into the output.

Python Multiplex will read the table input into a callback method. This method defines a size to each set of data that is sent on both outputs via a stream. It sends the data in batches until no more data are available on the input.

Both Terminals show the data that is being sent from the Python Operator. The Terminals output will be identical.



<a name="loiobba574eb699f4aadb4020d958a3b6ab8__section_usg_lrl_qrb"/>

## Create and Update Static Types

To use a different static data type in the Python Multiplex ports, you can create a custom type by following the steps below:

1.  Access the graph configuration and open the data types tab.

2.  Create or edit the data types.

3.  You will need to define ID, type, description, and properties to your data type.

4.  Save the data settings.

5.  Access the port configuration to change the data type ID. The custom data type and port must be the same type \(structure, table, or scalar\).




<a name="loiobba574eb699f4aadb4020d958a3b6ab8__section_gjr_qrl_qrb"/>

## See the Code for Python Operator

If you would like to see the code used for the operations, use the context menu "Open Script" of the Python Operator.

