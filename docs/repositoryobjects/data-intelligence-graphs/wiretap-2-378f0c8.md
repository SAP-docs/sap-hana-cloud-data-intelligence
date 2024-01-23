<!-- loio378f0c8681d642f382475e64e18649fd -->

# Wiretap 2

The Wiretap operator allows you to inspect messages that are transfered from one operator to another. This graph consists of two groups connected together and one script operator in group1 is emitting a sequence of "hallo" and two script operators in default group are emitting a sequence of "hello" and "hola", respectiely. Three Wiretap operators are monitoring those messages.



More precisely speaking:

-   script Hallo generates a series of hallo every 4 second in its own group of multiplicity 2, and its output is connected to wiretap3, and wiretap3 is connected to wiretap1.

-   script Hello generates a series of hello every second in its default group, and its output is connected to wiretap1 and wiretap2.

-   script Hola generates a series of hola every second in its default group, and its output is connected to wiretap2.




<a name="loio378f0c8681d642f382475e64e18649fd__section_r3z_hyt_w2b"/>

## Configure and Run the Graph

Follow the steps below to run the example from the Data Pipeline UI:

1.  Start the graph.
2.  Open the UI from wiretap1 and active the tabs for the other wiretaps.

The following output are expected:

-   wiretap1 shows a mixed series of hello and hallo.

-   wiretap2 shows a mixed series of hello and hola.

-   wiretap3 shows a series of hallo.

