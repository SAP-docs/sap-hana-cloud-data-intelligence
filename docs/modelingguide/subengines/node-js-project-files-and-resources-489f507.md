<!-- loio489f507c4b2e4db7923fc8823e9a3fe9 -->

# Node.js Project Files and Resources

Creating a Node.js operator requires a Node.js project file and other resources.

The resources in a Node.js project includes the following files:

-   vsolution.json
-   operator.json
-   script.js
-   README.md
-   operator icon \(\*.svg, \*.png, \*.jpeg\)



<a name="loio489f507c4b2e4db7923fc8823e9a3fe9__section_bgv_dm5_bhb"/>

## vsolution.json

The `vsolution.json` file describes the solution. The following script is an example `vsolution.json` file:

> ### Example:  
> ```
> {
>     "name": "vsolution_vflow_my_solution",
>     "version": "n.n.n",
>     "description": "my Solution",
>     "license": "my license"
> } 
> ```

**Increment the version number after every change.** If you don't increment the version number after every change, the SAP Data Intelligence system doesn't overwrite a deployed version.



<a name="loio489f507c4b2e4db7923fc8823e9a3fe9__section_ebx_ln5_bhb"/>

## operator.json

The `operator.json` specifies the base operator \(component\), the interface \(in ports, out ports\), configuration data, and other details of the operator. The following script is an example `operator.json` file:

> ### Example:  
> ```
> {
>   "component": "com.sap.node.operator", // extend the basic node operator
>   "description": "Operator description", // visible title of the operator in operators explorer in SAP Data Intelligence Modeler
>   "iconsrc": "icon.svg",
>   "inports": [
>     {
>       "name": "in1",
>       "type": "string"
>     }
>   ],
>   "outports": [
>     {
>       "name": "out1",
>       "type": "string"
>     }
>   ],
>   "config": {
>     "codelanguage": "javascript",
>     "script": "file://script.js"
>   }
> }
> ```

If the Node.js operator doesn't have any ports, you can omit the in ports and out ports, or leave them empty. If there is more than one port, the port names must be unique. In the unique port names, exclude special characters, such as white spaces.

You must specify the script configuration under the following circumstances:

-   You don't save the script file to the same root path as the `operator.json` file.
-   You name the script file differently than the operator name.

If you don't specify the script configuration under these circumstances, SAP Data Intelligence can leave the `operator.json` file out.



<a name="loio489f507c4b2e4db7923fc8823e9a3fe9__section_e3d_yn5_bhb"/>

## Operator Script

The `script.js` file is the entry point of your operator. The following sample code of a `script.js` file is from the operator 'Node.js Counter', which is also available in the SAP Data Intelligence Modeler:

> ### Example:  
> ```
> const SDK = require("@sap/vflow-sub-node-sdk");
> const operator = SDK.Operator.getInstance();
> let counter = 0;
> 
> /**
>  * This operator receives messages on port "in1",
>  * increases a counter and forwards the counter value
>  * to port "out1".
>  */
> operator.getInPort("in1").onMessage((msg) => {
>   // The content of the actual message is ignored.
>   // We will only count the number of messages here.
>   counter++;
>   operator.getOutPort("out1").send(counter.toString());
> });
> 
> /**
>  * A keep alive hook for the node process.
>  * @param tick length of a heart beat of the operator
>  */
> function keepAlive(tick) {
>   setTimeout(() => {
>     keepAlive(tick);
>   }, tick);
> }
> 
> // keep the operator alive in 1sec ticks
> keepAlive(1000);
> ```

Whenever the Node.js Counter operator receives a message at input port 'in1', it increments a counter and sends the current counter value to output port 'out1'. To prevent the Node.js process from terminating immediately after the start, a 'keepAlive' timer has been added. It resets a time-out every 1000 milliseconds.



<a name="loio489f507c4b2e4db7923fc8823e9a3fe9__section_qdd_k45_bhb"/>

## Operator Documentation

Create the operator's documentation in a file named `README.md` in the operator's folder.

> ### Example:  
> To create the documentation for the example operator named Counter, create a new `README.md` file in the following path:
> 
> ```
> my_solution/subengines/com/sap/node/operators/com/mydomain/util/counter/README.md
> ```

Use Markdown syntax to write the documentation. For more information about Markdown syntax, see [Basic Writing and Formatting Syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) in the GitHub documentation.



<a name="loio489f507c4b2e4db7923fc8823e9a3fe9__section_dfk_4p5_bhb"/>

## Operator Icon

You can add a custom icon \(file format: svg, .jpg or .png\) for your operator by copying the icon to the operator's folder:

> ### Example:  
> ```
> my_solution/subengines/com/sap/node/operators/com/mydomain/util/counter/icon.svg
> ```

