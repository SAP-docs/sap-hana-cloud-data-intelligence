<!-- loio20fad0ff7a3b4ffca67b52c446056059 -->

# Subengines

Subengines in the SAP Data Intelligence Modeler allow you to use operators for different runtimes apart from the main engine. The main engine coordinates graph and native operator executions.

Subengines allow a graph to contain operators that run as follows:

-   One operator runs in the main engine.
-   Other operators are implemented in Python and run in a Python subengine.
-   Other operators are implemented in C++ and run in the C++ subengine.

Operators can have implementations for more than one engine, including the main engine and subengines. With multiple engines, you can select a subset of the available engines in the operator's configuration panel from which the optimizer chooses. The optimizer assigns an engine for each operator to minimize the number of edges crossing different engines. When you schedule a cluster of connected operators to run in the same engine, all operators run in the same operating system process.

The available subengines in SAP Data Intelligence are:

-   ABAP
-   C++
-   Node.js
-   Python 3.9

> ### Note:  
> When you build a graph with subengines, communication between the engines incurs different communication costs.
> 
> > ### Example:  
> > A *File Consumer* operator runs only in the main engine. If a *File Consumer* operator sends data to the *Python3 Operator*, the Modeler must first serialize the data, send the data through a pipe to another operating system process, and finally deserialized the data.

Advantages of using subengines include the following:

-   Run connected operators that belong to the same subengine in a single process.

    Running in a single process is better than using the *Process Executor* operator that executes an external script to launch a new process for each operator.

-   Use scriptable operators in different languages, such as *Python3 Operator* and *Node Base Operator* on Node.js.

    Edit the scripts for these operators in the Modeler user interface without the requirement to handle serializing and deserializing outgoing and incoming data.

-   SAP can develop and deliver operators in programming languages other than the language used in the main engine.

-   Create and add new operators to the SAP Data Intelligence Modeler in different programming languages.

    For the Python subengine, you can extend the script operator *Python3 Operator* with new behavior. However, you can also develop new operators in your own machine, and then upload the new operators to the cluster through SAP Data Intelligence System Management. For more information about the Python subengine, see [Create Operators with the Python Subengine](create-operators-with-the-python-subengine-7e8f7d2.md).


-   **[Working with the C++ Subengine to Create Operators](working-with-the-c-subengine-to-create-operators-d8f634c.md "The SAP Data Intelligence Modeler C++ subengine lets
		you code your own operators in C++ and make them available for use from the Modeler application.")**  
The SAP Data Intelligence Modeler C++ subengine lets you code your own operators in C++ and make them available for use from the Modeler application.
-   **[Create Operators with the Python Subengine](create-operators-with-the-python-subengine-7e8f7d2.md "Create operators in Python using the Python subengine, and use them to build graphs in the SAP Data Intelligence Modeler. ")**  
Create operators in Python using the Python subengine, and use them to build graphs in the SAP Data Intelligence Modeler.
-   **[Working with the Node.js Subengine to Create Operators](working-with-the-node-js-subengine-to-create-operators-2f89f14.md "Use the Node.js subengine to code custom operators in a specified programming language to use in the SAP Data Intelligence Modeler application.")**  
Use the `Node.js` subengine to code custom operators in a specified programming language to use in the SAP Data Intelligence Modeler application.
-   **[Working with Flowagent Subengine to Connect to Databases](working-with-flowagent-subengine-to-connect-to-databases-f190a28.md "Partitioning the source data allows us to load data in chunks there by overcome memory
		pressure and by doing it in parallel we can load data faster and improve overall
		performance. ")**  
Partitioning the source data allows us to load data in chunks there by overcome memory pressure and by doing it in parallel we can load data faster and improve overall performance.

**Related Information**  


[SAP Data Intelligence Operators](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/acd32810819a4b2893c9f8698e2ec55c.html "SAP Data Intelligence provides built-in operators, that you can use directly in a graph or as the basis for creating a custom operator.") :arrow_upper_right:

