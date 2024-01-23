<!-- loio805f652911004597892c1aa89841dc8f -->

# Histogram Simple Example

In this simple graph, the first operator generates random numbers that are sent to the Histogram operator. The Histogram operator produces the histogram of its inputs as a Message with an integer array on its body and the range of the interval on its attributes. The message is then converted to string by the ToString Converter and sent to the HistogramPlotter, which finally plots it in the user interface.



This is a linear graph where the first operator is a Javascript operator that generates a random float number between 0 and 20 every 1 second. This float is sent to the Histogram operator that will produce an array of uint64, representing the histogram, each time it receives an input.

In this graph, the Histogram operator is configured with nBins=5, rangeMin=2, and rangeMax=19. This means that the outputted histogram array will have size 5 and the interval \(2, 19\) will be evenly distributed over the array's cells. That is, each cell will cover a subinterval of length \(19-2\)/5=3.4.

The bin of index 0 counts the inputs between 2 and 5.4, index 1 between 5.4 and 8.8, index 2 between 8.8 and 12.2, index 3 between 12.2 and 15.6, and index 4 between 15.6 and 19. Inputs received outside the range 2 and 19 will not be counted in any bin.

The output of the Histogram operator is a Message with the histogram array on its body and the rangeMin and rangeMax values on its attributes. This is sent to the ToString Converter, which will convert the Message to its string representation. This string representation is then fed into the Histogram Plotter operator, which shows a visual representation of the histogram that can be seen by clicking on the *Open UI* button on this operator.

