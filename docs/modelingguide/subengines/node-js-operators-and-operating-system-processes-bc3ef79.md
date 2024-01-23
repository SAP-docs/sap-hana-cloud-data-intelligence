<!-- loiobc3ef79ca0f144b7aca66aa81f0f4c8b -->

# Node.js Operators and Operating System Processes

Every `Node.js` operator runs in its own operating system process, which allows the `Node.js` subengine to use multicore CPUs and parallel system architectures.

Running `Node.js` operators in their own operating system provides isolation between `Node.js` operators for enhanced security.

`Node.js` processes communicate by TCP socket-based IPC \(interprocess communication\), which is coordinated by the `Node.js` subengine. In turn, the `Node.js` subengine runs in its own process. There's one coordinating `Node.js` subengine process per subgraph that consists of only `Node.js` operators.

> ### Note:  
> All multiplexers run directly in the `Node.js` subengine process, which reduces communication overhead. Therefore, ensure that you set the *Subengine* to `com.sap.node` in the `Node.js` subgraph configuration pane. Otherwise, the subgraph divides into two `Node.js` subgraphs with a multiplexer in between running in Go or another subengine.

> ### Example:  
> A subgraph consists of 10 `Node.js` operators. Three of the nodes are multiplexer. The multiplexer nodes are configured to run in subengine `'com.sap.node'`. The number of operating system processes computes to eight operating system processes as follows:
> 
> ```
> 1 (Node.js Subengine) + 10 (Node.js operators) - 3 (Node.js Multiplexer) = 8 operating system processes.
> ```
> 
> > ### Note:  
> > A graph can result in multiple `Node.js` subgraphs, depending on which operators are interconnected.

