<!-- loio2f89f14fcfe742d3bde0a4ee19a0f195 -->

# Working with the Node.js Subengine to Create Operators

Use the `Node.js` subengine to code custom operators in a specified programming language to use in the SAP Data Intelligence Modeler application.

The `Node.js` subengine runs `Node.js` operators with other operators designed for different platforms, like Go, Python, and C++. The `Node.js` subengine runs individual operators or entire subgraphs. The more you directly interconnect `Node.js` operators, the bigger the pure `Node.js` subgraph.

The `Node.js` subengine provides the following features:

-   Use modern JavaScript, such as ECMAScript V6, to develop operators.

-   Use the Node JavaScript runtime environment built on Google Chrome V8.

-   Use your preferred language that can be compiled into JavaScript, such as TypeScript.

-   Use your own requried set of third-party libraries.


-   **[Node.js Operators and Operating System Processes](node-js-operators-and-operating-system-processes-bc3ef79.md "Every Node.js operator runs in its own operating system process, which allows the Node.js
		subengine to use multicore CPUs and parallel system architectures.")**  
Every `Node.js` operator runs in its own operating system process, which allows the `Node.js` subengine to use multicore CPUs and parallel system architectures.
-   **[Use Cases for the Node.js Subengine](use-cases-for-the-node-js-subengine-635db3c.md "There are two use cases for the Node.js subengine: Use the Node.js subengine in the SAP Data Intelligence Modeler application, or use a
		dedicated local Node.js project to develop a Node.js operator.")**  
There are two use cases for the Node.js subengine: Use the Node.js subengine in the SAP Data Intelligence Modeler application, or use a dedicated local Node.js project to develop a Node.js operator.
-   **[The Node.js Subengine SDK](the-node-js-subengine-sdk-706e4ca.md "The Node.js subengine SDK module simplifies the development of Node.js operators.")**  
The Node.js subengine SDK module simplifies the development of Node.js operators.
-   **[Node.js Data Types](node-js-data-types-402e6b6.md "SAP Data Intelligence maps Modeler data types to the
		Node.js JavaScript data types.")**  
SAP Data Intelligence maps Modeler data types to the Node.js JavaScript data types.
-   **[Node.js Safe and Unsafe Integer Data Types](node-js-safe-and-unsafe-integer-data-types-33cefca.md "Because JavaScript doesn't have an integer data type, there are safe and unsafe integer data types when you use the Node.js subengine. ")**  
Because JavaScript doesn't have an integer data type, there are safe and unsafe integer data types when you use the Node.js subengine.
-   **[Create a Node.js Operator](create-a-node-js-operator-f72f19c.md "Create Node.js operators using a dedicated Node.js project.")**  
Create Node.js operators using a dedicated Node.js project.
-   **[Node.js Project Structure](node-js-project-structure-fd151b1.md "To deploy a Node.js operator to an To deploy your operator later to a different SAP Data Intelligence system, create a project structure. ")**  
To deploy a Node.js operator to an To deploy your operator later to a different SAP Data Intelligence system, create a project structure.
-   **[Node.js Project Files and Resources](node-js-project-files-and-resources-489f507.md "Creating a Node.js operator requires a Node.js project file and other resources.")**  
Creating a Node.js operator requires a Node.js project file and other resources.
-   **[Node.js Subengine Logging](node-js-subengine-logging-d6fd4ce.md "The logging library provides different logging APIs that propagate logging information to the Node.js subengine. In local development that
		isn't running with Node.js subengine core, the console is used for logging.")**  
The logging library provides different logging APIs that propagate logging information to the Node.js subengine. In local development that isn't running with Node.js subengine core, the console is used for logging.

