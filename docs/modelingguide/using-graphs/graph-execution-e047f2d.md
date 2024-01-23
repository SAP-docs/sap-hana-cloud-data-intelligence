<!-- loioe047f2db30774d67bb5fe68d3c369396 -->

# Graph Execution

The Modeler application supports executing a graph and monitoring its status from within the application.

When you schedule a graph for execution, the application translates the graphical representation \(internally represented as a JSON document\) into a set of running processes. These processes are responsible for the graph execution.

During the graph execution, the application translates each operator in the graph into \(server\) processes and translates the input and output ports of the operators into message queues. The process runs and waits for an input message from the message queue \(input port\). When it receives the input message, it starts processing to produce an output message and delivers it to the outgoing message queue \(output port\). If a message reaches a termination operator, the application stops executing all processes in the graph and the data flow stops.

> ### Note:  
> If a graph does not have a graph terminator operator, it continues to execute all processes until you manually stop the graph execution.

