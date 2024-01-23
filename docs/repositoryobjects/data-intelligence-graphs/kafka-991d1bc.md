<!-- loio991d1bcae580465488cdc3abd121a33e -->

# Kafka

The data generator generates arbitrary data and passes it to the Kafka producer. The Kafka consumer reads the data and writes it to a terminal. You can see the generated data by opening the UI of the terminal operator.



## Prerequisites

-   A running Kafka broker and Zookeeper .



<a name="loio991d1bcae580465488cdc3abd121a33e__section_rzy_lnb_t2b"/>

## Configure and Run the Graph

1.  In the left panel, select the *Graphs* tab and navigate to `com/sap/demo/kafka`.
2.  Check the configuration of the *producer \(20fb\) node*: brokers
3.  Check the configuration of the *consumer \(1h7j\) node*: zookeepers
4.  In the tool bar, select *Run* \(play button\).
5.  The *Status* panel indicates if the graph is running.
6.  Use the context menu *Open UI* of the *terminal \(z8d\)* node to open the terminal.
7.  The terminal opens and you see the generated data.

