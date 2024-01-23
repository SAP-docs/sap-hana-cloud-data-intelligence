<!-- loio84e1df1ac115413da64b622ca779a424 -->

# Using Operators

Operators represent vertexes in a graph \(pipeline\) and are components that react to events configured in the graph environment.

Events are messages delivered to the operator through input ports. An operator interacts with the graph environment through its output ports. The operator is unaware of the graph in which it's defined and the source and target of its incoming and outgoing connections.

> ### Note:  
> Events can also be internal to the operator, such as clock ticks.

The following image shows an operator with input and output ports. Each port has a type. SAP Data Insight Modeler color codes the ports to indicate compatible port types.

![](images/operators11_72f52ea.png)

For complete information about operators in SAP Data Intelligence Modeler, see the *Repository Objects Reference*.

-   **[Operator Details](operator-details-2a647f3.md "Every operator has an ID (also known as name) and a title (also known as the description). The operator ID is a unique identifier, with a
		strict format. The operator title is what the graphical interface displays.")**  
Every operator has an ID \(also known as name\) and a title \(also known as the description\). The operator ID is a unique identifier, with a strict format. The operator title is what the graphical interface displays.
-   **[Generation 1 and Generation 2 Operators](generation-1-and-generation-2-operators-1c97a10.md "SAP Data Insight Modeler offers two generations of operators: Generation 1 (Gen1) and Generation 2 (Gen2).")**  
SAP Data Insight Modeler offers two generations of operators: Generation 1 \(Gen1\) and Generation 2 \(Gen2\).
-   **[Customizing the List of Operators](customizing-the-list-of-operators-0cb2a5b.md "Limit the list of operator categories in the Operators tab to include only the operators that you use.")**  
Limit the list of operator categories in the *Operators* tab to include only the operators that you use.
-   **[Ports and Port Types](ports-and-port-types-6789999.md "The operator uses ports as an interface to communicate between operators in a
		graph.")**  
The operator uses ports as an interface to communicate between operators in a graph.
-   **[Using Managed Connections in Script Operators](using-managed-connections-in-script-operators-90037ee.md "You can use managed connections in operator configurations of the script operators.")**  
You can use managed connections in operator configurations of the script operators.
-   **[Creating Operators](creating-operators-049d2f3.md "Use the SAP Data Intelligence Modeler to create your own operators to use in graphs (pipelines). ")**  
Use the SAP Data Intelligence Modeler to create your own operators to use in graphs \(pipelines\).
-   **[Configuring Operators](configuring-operators-e9c9996.md "Each operator has parameters that you can configure based on the business requirements for the graph (pipeline). ")**  
Each operator has parameters that you can configure based on the business requirements for the graph \(pipeline\).
-   **[Creating Categories](creating-categories-9f64ea7.md "Create a custom category for the operators or graphs that you create.")**  
Create a custom category for the operators or graphs that you create.
-   **[Creating Operator Groups](creating-operator-groups-f500f5c.md "Partition a graph into subgroups so that each subgroup runs in a different Docker container assigned to different cluster
		nodes.")**  
Partition a graph into subgroups so that each subgroup runs in a different Docker container assigned to different cluster nodes.
-   **[Viewing Operator Versions](viewing-operator-versions-f1007e1.md "You can view all existing versions, modify existing versions, or create additional versions of an operator. You can also replace a
		deprecated operator with the alternative operator and maintain logs for respective versions of an operator.")**  
You can view all existing versions, modify existing versions, or create additional versions of an operator. You can also replace a deprecated operator with the alternative operator and maintain logs for respective versions of an operator.
-   **[Editing Operators](editing-operators-e1120eb.md "You can modify the existing operators and use them in your graph. The Modeler provides a form-based editor to make changes to the
		operators.")**  
You can modify the existing operators and use them in your graph. The Modeler provides a form-based editor to make changes to the operators.
-   **[Error Handling in Generation 2 Operators](error-handling-in-generation-2-operators-b88468d.md "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.")**  
The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.
-   **[Batch Header](batch-header-40e5f8d.md "Operators use batch headers to express information about its output batches in a unified way.")**  
Operators use batch headers to express information about its output batches in a unified way.
-   **[State Management](state-management-1d2d1aa.md "Use the state management feature by implementing a series of functions in the Python3 operator. ")**  
Use the state management feature by implementing a series of functions in the Python3 operator.
-   **[Dockerfile Library for Runtime Environment](dockerfile-library-for-runtime-environment-163f5d9.md "Operators require a certain runtime environment. For example, if an operator executes some JavaScript code, then the operator requires an
		environment with a JavaScript engine.")**  
Operators require a certain runtime environment. For example, if an operator executes some JavaScript code, then the operator requires an environment with a JavaScript engine.

**Related Information**  


[Ports and Port Types](ports-and-port-types-6789999.md "The operator uses ports as an interface to communicate between operators in a graph.")

[Graph Execution](../using-graphs/graph-execution-e047f2d.md "The Modeler application supports executing a graph and monitoring its status from within the application.")

[Creating Operators](creating-operators-049d2f3.md "Use the SAP Data Intelligence Modeler to create your own operators to use in graphs (pipelines).")

