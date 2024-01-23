<!-- loioc452e2fc895442ab9a7939b4f27174cb -->

# Multiplexer for Dynamic Inputs

This scenario showcases how to read dynamic data from more than one input and write to one output using a Python Operator.



Both Python Generators generate an example table and send it as data into the output.

The Python Multiplex reads each of the inputs that are receiving data into a callback method. This method defines a size to each set of data that is sent on the output via a stream. It sends the data in batches until no more data are available on the input.

The Terminal shows all data received from the Python Operator.



<a name="loioc452e2fc895442ab9a7939b4f27174cb__section_pxs_3ql_qrb"/>

## See the Code for Python Operator

If you would like to see the code used for the operations, use the context menu "Open Script" of the Python Operator.

