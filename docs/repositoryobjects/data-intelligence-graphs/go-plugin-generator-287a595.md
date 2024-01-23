<!-- loio287a5953ef134426a8d34ae4f1fdc813 -->

# Go Plugin Generator

The Go operator allows a custom Go program to be compiled and dynamically loaded into a running Pipeline scenario.



Unfortunately, there is a limitation in the Go operator that it can only build a plugin library when there are no external package dependencies in the source code.

This limitation results in the error message:

```
plugin.Open("..."): plugin was built with a different version of package ...
```

Until this limitation is resolved, this graph can be used to build the compatible plugin libraries for a graph that contains Go programs with external package dependencies.

> ### Note:  
> When the imported external library is already used by the pipeline engine, the version cannot be changed.



<a name="loio287a5953ef134426a8d34ae4f1fdc813__section_i5n_tmt_jpb"/>

## Prerequisites

None.



<a name="loio287a5953ef134426a8d34ae4f1fdc813__section_j1b_wmt_jpb"/>

## Configure and Run the Graph

Follow the steps below to run this graph from the Data Pipeline UI:

1.  Go to the configuration panel for operator Go Plugin Generator.

2.  Set the property *Graph name* to the ID of the graph you want to generate the plugin library for. If this property is not visible in the configuration panel, open the JSON view of the configuration and look for the *config* property of the operator with ID gooperator1. Set its property `graphName` manually.

3.  Save the graph.

4.  Start the graph to generate the plugin library for the target graph.

5.  After the graph successfully terminates, open and start the target graph.

    In this particular graph, this operator is connected to operator Terminator\(ID:graphterminator1\), and as a result, this graph will terminate upon a successful plugin generation. If you wish to automatically start the target graph, connect the operator OpenAPI Client instead of Terminator. In this case, the connection properties of the OpenAPI Client must be set accordingly.


