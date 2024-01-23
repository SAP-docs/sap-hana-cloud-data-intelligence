<!-- loio635db3c48c62404cb549ef260dbb2d38 -->

# Use Cases for the Node.js Subengine

There are two use cases for the Node.js subengine: Use the Node.js subengine in the SAP Data Intelligence Modeler application, or use a dedicated local Node.js project to develop a Node.js operator.

The Node.js subengine consists of two major building blocks:

-   Node.js subengine core
-   Node.js Subengine SDK

While you probably never work directly with the core engine, you'll work with the Node.js Subengine SDK to develop your operators. For more information about the SDK, see [The Node.js Subengine SDK](the-node-js-subengine-sdk-706e4ca.md).



<a name="loio635db3c48c62404cb549ef260dbb2d38__section_v1q_zdv_xyb"/>

## Use Node.js in the Modeler

Using the SAP Data Intelligence Modeler is the easiest way to change or add graph functionality quickly. Just add a Node.js Script operator to existing graphs, or modify the JavaScript code of existing Node.js script operators.

> ### Note:  
> The only external node-module that can be required inside the SAP Data Intelligence Modeler is `'@sap/vflow-sub-node-sdk'`.



<a name="loio635db3c48c62404cb549ef260dbb2d38__section_cmj_b2v_xyb"/>

## Use Node.js in a Dedicated Project

To develop a Node.js operator, use a dedicated local Node.js project. Using a dedicated project allows you to use your own tools and frameworks, and code Node.js operators like any other Node.js program.

Some of the advantages of using a dedicated project include the following:

-   Use JavaScript libraries that you've already created.
-   Use your own required set of third-party node modules.
-   Use test driven development.
-   Use other languages that compile to JavaScript, such as TypeScript.

**Related Information**  


[Availability of the Node.js Subengine SDK](availability-of-the-node-js-subengine-sdk-de1481f.md "The Node.js SDK is included into the Node.js subengine, but you can also download and install it.")

