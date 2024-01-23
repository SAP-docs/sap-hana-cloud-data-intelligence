<!-- loio3407cb7ffe944918b31dcb2d4c9fac98 -->

# Simple Command Executor

In this simple graph the first 2 operators \(Data Generator and ToBlobConverter\) generate blobs, which are send to the input port `stdin` of the Command Executor. The Command Executor executes a build-in Unix command on the input and pipes the result to the output port `stdout`. The resulting blob can be visualized using the connected Wiretap operator. If an error occurs in the command executor it is send via the second output port `stderr` to terminate the graph.



<a name="loio3407cb7ffe944918b31dcb2d4c9fac98__section_xsp_5d3_rrb"/>

## Prerequisites

None.



<a name="loio3407cb7ffe944918b31dcb2d4c9fac98__section_c2t_vd3_rrb"/>

## Description

The first operator is a simple string generator which generates a series of English phrases and sends them to the `ToBlobConverter` to have convert them into a blob. In practice this could be replaced by any other source for a large binary object. For example, the data could also be fetched from a `VARBINARY` column of a database or be the result of some serialization.

The Command Executor is similiar to the Process Executor. They both wrap the standard IO of the operating system. While the Process Executor works with ports of type `stream`, the Command Executor connects input and output of type `blob` instead. In any case both operators accept a command line instruction in the configuration. In this example it is just the shell hex dump utility which outputs \(with the `-C` option\) the hexadecimal and ASCII representation of the input. Alternatively any other program which is known in the execution environment can be executed. Use cases could be special transformations, which can not easily be reimplemented using some scripting. It is worth noting that forking of process or similar is not supported here. In case of errors they can either be sent to the second outport `stderr` which is bound to the OS standard error or they can be sent to the trace.

In this example the `stderr` port is connected to a graph terminator, that is the first error would lead to the termination of the graph. The `stdout` port is connected to the Wiretap operator. The output can be seen clicking on the “Open UI” button in the context menu of the operator. In practice the blob data would be passed on for further processing.

