<!-- loio604dc688a7fa4969b74bb4b9bfa97730 -->

# Wiretap 3

The Wiretap operator allows you to inspect messages that are transfered from one operator to another. This graph consists of two parts: one part with group multiplicity of 2, each generating its own series of data and monitoring the data at the first Wiretap opeator Wiretap1 \(ID:wiretap1\), which in turn is connected to the second Wiretap operator Wiretap2 \(ID:wiretap2\) in the default group.



The Javascript operator Datagenerator \(ID:javascriptv2operator1\) is generating a series of hi-n, where n is a monotonically increasing integer number. The layout property of both Wiretap operators are set to `[%i@node-%g] %m`, which results in each line prefixed with the received index and the worker name.



<a name="loio604dc688a7fa4969b74bb4b9bfa97730__section_r3z_hyt_w2b"/>

## Prerequisites

-   A cluster instance to run this graph with multiple workers.




<a name="loio604dc688a7fa4969b74bb4b9bfa97730__section_ozn_fwx_smb"/>

## Configure and Run the Graph

Follow the steps below to run the example from the Modeler:

1.  Start the graph;

2.  Open the UI from Operator Wiretap1 and active the tab for wiretap2 so that both tabs wiretap1 and wiretap2 are shown.

The following output is expected:

-   wiretap1 is placed in the group with multiplicity of 2. Therefore, it shows two series of sequences: one with `@node-group1-0` and the other with `@node-group1-1`, where each with its own incremental sequence of hi-n should look like:


```
[0@node-group1-0] hi-0
[1@node-group1-0] hi-1
[2@node-group1-0] hi-2
[3@node-group1-0] hi-3
[4@node-group1-0] hi-4
[5@node-group1-0] hi-5
[0@node-group1-1] hi-0
[1@node-group1-1] hi-1
[2@node-group1-1] hi-2
[3@node-group1-1] hi-3
[4@node-group1-1] hi-4
[5@node-group1-1] hi-5
[6@node-group1-1] hi-6
[6@node-group1-0] hi-6
[7@node-group1-0] hi-7
[7@node-group1-1] hi-7
[8@node-group1-0] hi-8
[8@node-group1-1] hi-8
[9@node-group1-0] hi-9
[9@node-group1-1] hi-9
[10@node-group1-0] hi-10
...
```

In contrast, wiretap2 is placed in the default group. Therefore, it shows a single sequence of data prefixed with `@node-default`, which should look like:

```
[0@node-default] hi-0
[1@node-default] hi-0
[2@node-default] hi-1
[3@node-default] hi-1
[4@node-default] hi-2
[5@node-default] hi-2
[6@node-default] hi-3
[7@node-default] hi-3
[8@node-default] hi-4
[9@node-default] hi-4
[10@node-default] hi-5
[11@node-default] hi-5
[12@node-default] hi-6
[13@node-default] hi-6
[14@node-default] hi-7
[15@node-default] hi-7
[16@node-default] hi-8
[17@node-default] hi-8
[18@node-default] hi-9
[19@node-default] hi-9
[20@node-default] hi-10
[21@node-default] hi-10
...
```

