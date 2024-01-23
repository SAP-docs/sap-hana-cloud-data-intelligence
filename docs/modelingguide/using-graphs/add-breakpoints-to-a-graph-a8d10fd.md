<!-- loioa8d10fdb5702453fa39ae2c47240debb -->

# Add Breakpoints to a Graph

Breakpoints and streaming points allow you to inspect the data transformation occurring throughout the pipeline when you run in *Debug* mode.



## Context

When running in debug mode, streaming points will be set by default in all connections. You will be able to convert streaming points to breakpoints, which stops when data hits them and shows visually. You can modify or resume execution of that connection, which in turn would stop again when data hits the next connection breakpoint.

You can set a breakpoint during design time or run time. The design time breakpoints will not be saved with graph information, which means that design time breakpoints gets reset once you close and open the graph again.



## Procedure

1.  To set a breakpoint,

    -   hover over the connection between operators in a graph, you will get an option to click and set the breakpoint.

        or

    -   right-click over the connection between operators in a graph and click *Add Breakpoint*.

2.  Run the graph in debug mode. For more information, see [Debug Graphs](debug-graphs-06b0159.md).

3.  To add/remove breakpoints, right-click a breakpoint in the debug panel or in the graph and select the appropriate option in the context menu.

4.  For a breakpoint, you can:

    1.  inspect and modify data upon hit. Right-click and select *Inspect Data* in the context menu.

    2.  resume inspection. Right-click and select *Resume* in the context menu.


5.  For a streaming point, you can:

    1.  open its corresponding debugger page. Right-click and select *Open Streaming UI*.



