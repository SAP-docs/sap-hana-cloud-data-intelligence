<!-- loio61af45d689624e93a686ef0157209bd2 -->

# Jupyter Example

This is an example graph for using a Jupyter operator. It illustrates how a Jupyter operator can be used to interact with data flowing through the graph.



The graph is composed of the following components:

-   Py3 Data Generator: Generates random sample data every 500ms.

-   Jupyter operator: Can be used to interact with the received data from the Py3 Data Generator. In this particular example, the operator has an input port called “in” and an output port called “out”.

-   Terminal: The terminal can be used in this graph to see the outputs from the Jupyter operator.




<a name="loio61af45d689624e93a686ef0157209bd2__section_hns_s24_k4b"/>

## Prerequisites

This text assumes the reader has already read the Jupyter operator documentation.



<a name="loio61af45d689624e93a686ef0157209bd2__section_lx4_1f4_k4b"/>

## Running the Graph

1.  Run the graph.

2.  Right-click on the Jupyter operator and select *Open UI*. You are redirected to a notebook with basic examples and the documentation of the predefined functions.

3.  Run the first code cell, the example on how to write data to output ports.

4.  Verify that the data was written to the output port. Go back to the graph, right-click on the Terminal operator and select *Open UI*. You should see the data on the terminal’s UI.

5.  Go back to the notebook and play with the examples and code samples.


