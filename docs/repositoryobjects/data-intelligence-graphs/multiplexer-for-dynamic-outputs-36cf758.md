<!-- loio36cf7585abb84295922d7dc1fe4ea9d7 -->

# Multiplexer for Dynamic Outputs

This scenario showcases how to read dynamic data from an input and write to multiple outputs using a Python Operator.



Python Generator generates an example table and sends it as data into the output.

Python Multiplex will read the table input into a callback method. This method defines a size to each set of data that is sent on both outputs via a stream. It sends the data in batches until no more data are available on the input.

Both Terminals show the data that is being sent from the Python Operator. The Terminals output will be identical.



<a name="loio36cf7585abb84295922d7dc1fe4ea9d7__section_dhd_qql_qrb"/>

## See the Code for Python Operator

If you would like to see the code used for the operations, use the context menu "Open Script" of the Python Operator.

