<!-- loiof72f19cde9ba441b919ce15819453ca4 -->

# Create a Node.js Operator

Create Node.js operators using a dedicated Node.js project.



<a name="loiof72f19cde9ba441b919ce15819453ca4__prereq_jkn_nmj_tyb"/>

## Prerequisites

You must be a cluster administrator to perform this task.

Before performing the following steps, download the Node.js subengine SDK from an SAP Data Intelligence System. For more information, see [The Node.js Subengine SDK](the-node-js-subengine-sdk-706e4ca.md).



## Procedure

1.  Log in to SAP Data Intelligence System Management as a cluster administrator.

2.  Open *Files* and then open *Union View*.

3.  Expand the following nodes: *files/vflow/subengines/com/sap/node*.

4.  Select `vflow-sub-node-sdk.tar.gz` and choose the *Export files or solutions* icon in the toolbar.

5.  Export the file to your local Node.js project. Save it to an appropriate location inside your project.

6.  Install the SDK file `vflow-sub-node-sdk.tar.gz` using the Node.js package manager so that it's available to your JavaScript code.

    ```
    npm install --save [path_to]/vflow-sub-node-sdk.tar.gz
    ```

7.  Check that the export added the `(runtime-)` dependency to your `package.json`.

    ```
    {
    	"name": …,
    	"version": …,
    	"dependencies": {
    		"@sap/vflow-sub-node-sdk": "file:vflow-sub-node-sdk.tar.gz",
    		…
    	}
    }
    ```

8.  **Optional:** Personalize the `Node.js` operator behavior in the Modeler in one of the following ways:


    <table>
    <tr>
    <th valign="top">

    Method
    
    </th>
    <th valign="top">

    Directions
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    **Use Node.js Script operator**
    
    </td>
    <td valign="top">
    
    The edited script using this method is specific to the given graph and operator instance.

    1.  Drag and drop the `Node.js Script` operator to the graph canvas in the Modeler.
    2.  Open the script editor.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Create a new operator**
    
    </td>
    <td valign="top">
    
    The advantage of the following method is that you can reuse the new operator across many graphs.

    1.  Create a new operator in a select subfolder in the Operators node of the *Repository* tab.
    2.  Choose **Node Base Operator** for *Base Operator* in the *Create Operator* dialog box.
    3.  Create input and output ports, tags, configuration parameters, and custom script as necessary.


    
    </td>
    </tr>
    </table>
    

-   **[Requiring Node Modules](requiring-node-modules-01e8113.md "A Node.js operator runs in its own process, therefore, it can also require its own individual set and version of node modules.")**  
A Node.js operator runs in its own process, therefore, it can also require its own individual set and version of node modules.

