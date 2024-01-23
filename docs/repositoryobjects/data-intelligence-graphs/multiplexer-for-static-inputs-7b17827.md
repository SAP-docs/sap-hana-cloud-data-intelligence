<!-- loio7b17827bb2bf44798027d810c3e20e51 -->

# Multiplexer for Static Inputs

This scenario showcases how to read static data from more than one input and write to one output using a Python Operator.



Both Python Generators generate an example table and send it as data into the output.

Python Multiplex will read each of the inputs that are receiving a table into a callback method. This method defines a size to each set of data that is sent on the output via a stream. It sends the data in batches until no more data are available on the input.

The Terminal shows all data sent from the Python Operator.



<a name="loio7b17827bb2bf44798027d810c3e20e51__section_obx_vql_qrb"/>

## Create and Update Static Types

To use a different static data type in the Python Multiplex ports, you can create a custom type by following the steps below:

1.  Access the graph configuration and open the data types tab.

2.  Create or edit the data types.

3.  You will need to define ID, type, description, and properties to your data type.

4.  Save the data settings.

5.  Access the port configuration to change the data type ID. The custom data type and port must be the same type \(structure, table, or scalar\).




<a name="loio7b17827bb2bf44798027d810c3e20e51__section_r3t_1rl_qrb"/>

## See the Code for Python Operator

If you would like to see the code used for the operations, use the context menu "Open Script" of the Python Operator.

