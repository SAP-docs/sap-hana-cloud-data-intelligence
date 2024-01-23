<!-- loio049d2f3cc69c4281a3f4570c0d2d066e -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Creating Operators

Use the SAP Data Intelligence Modeler to create your own operators to use in graphs \(pipelines\).



<a name="loio049d2f3cc69c4281a3f4570c0d2d066e__prereq_rwx_f5p_1xb"/>

## Prerequisites

Before you create a new operator, ensure that you choose an existing folder in the repository or create a new folder. Create a new folder in the Modeler as follows:

1.  Open the *Repository* tab in the Navigation pane at left.
2.  Expand the *Operators* folder.
3.  Right-click the operators folder and choose *Create Folder*.



## Context

The Modeler provides a form-based editor to create operators. An operator is a reactive component, which means that it reacts to events from the environment. It isn't intended to terminate. The operators that you create in the Modeler are derived from the base operators that the application provides.



## Procedure

1.  Right-click the applicable folder choose *Create Operator*.

    The *Create Operator* dialog box opens.

2.  Enter the fully qualified path and file name in *Name*.

3.  Enter a name by which the operator is listed in *Display Name*.

    The Modeler lists the operator by this name in the *Operators* tab. Also, use the name to search for the operator in the Modeler.

4.  Choose the applicable base operator from the *Base Operator* list.

    The base operators listed are derived from the built-in base operators provided by SAP Data Intelligence.

5.  Choose the category in which to create the operator from the *Category* list and select *OK*.

    Use the category as a search tool in the navigation pane.

    The Modeler opens the operator editor in the main pane. There are several tabs in which you create the operator properties: *Ports*, *Tags*, *Configuration*, *Script*, and

6.  Define the operator using the various tabs in the operator editor. The following table describes actions for each tab.


    <table>
    <tr>
    <th valign="top">

    Action
    
    </th>
    <th valign="top">

    Steps
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Define ports
    
    </td>
    <td valign="top">
    
    1.  Open the *Ports* tab.
    2.  Select :heavy_plus_sign:
    3.  Enter a port name in *Name*.
    4.  Choose a type in *Data Type*.
    5.  Continue adding input or output ports in this manner as necessary.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Define tags
    
    </td>
    <td valign="top">
    
    Tags describe the runtime requirements of operators and are the annotations of Dockerfiles that the application provides. If multiple implementations exist for the operator, the application displays the different subengines in which you can execute the operator. For each subengine, you can further associate them with tags from the database.

    1.  Open the *Tags* tab.
    2.  Select :heavy_plus_sign:.
    3.  Choose a tag from *Tags*.
    4.  Choose a version from *Version*.
    5.  Continue adding tags in this manner as necessary.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Define configurations
    
    </td>
    <td valign="top">
    
    The options in the *Configuration* tab vary based on the type of operator you're creating.

    1.  Open the *Configuration* tab.

        The original schema name appears under Schema File. You can change the parameters of the schema file by automatic generation or by importing. To enable the automatic or import feature, select :wastebasket:

    2.  For automatic generations, select *Generate Config Schema*.
    3.  To import, select *Import*.
    4.  To edit the schema, select :pencil2:to open the *Edit type* dialog box.

        Types allow you to enable semantic type validations on top of the configuration parameters and to define conditions. Create new types or edit existing type definitions in the repository. Reuse existing types to define the operator configuration.

        > ### Note:  
        > By default, the type definition of script-based operators such as JavaScript, Python, Go operators, and so on, include a *Script* property. Use this property to view or modify the operator script when creating a graph. To hide the script from users working with this operator, edit the *Script* property in the type schema. Select the property and set the *Visibility* value to *Hidden*.

    5.  Select a property to edit and view the parameters to the right.
    6.  Add additional parameters by selecting :heavy_plus_sign:

        Provide the configuration parameter name, select the parameter type, and provide a parameter value.

        > ### Remember:  
        > For some base operators, the application doesn't allow you to define new configuration parameters. If you aren't allowed to define new parameters, :heavy_plus_sign: is disabled, and you can only edit the existing parameter values.



    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Add scripts
    
    </td>
    <td valign="top">
    
    In graphs, use operators that help run script snippets when the graph runs. To include script snippets in the operator definition, perform the following steps:

    1.  Open the *Script* tab.
    2.  Enter the script snippet in the *Inline Editor*.
    3.  To change the default programming language of the editor, choose a different language in the upper right. This option isn't always available.
    4.  To upload a script file from your system, choose *Upload File* from the list in the top-left corner of the editor and select<span class="SAP-icons"></span> \(Upload file\) at right.


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Add operator documentation
    
    </td>
    <td valign="top">
    
    Maintain or modify documentation for operators in the *Documentation* tab. Documentation contains information about the operator configuration parameters, input ports, output ports, and more. Adding documentation helps other users when working with this operator.

    1.  Open the *Documentation* tab.
    2.  Enter the required documentation in the text area.

        > ### Tip:  
        > SAP recommends that you use the Markdown format to maintain the operator documentation.



    
    </td>
    </tr>
    </table>
    
7.  **Optional:** Select a display icon for the operator.

    In the operator editor, the Modeler displays the operator name with a generic icon. You can replace the display icon with any of other icons that the application provides, or you can upload your own icon in Scalable Vector Graphics \(SVG\) format and use it for the operator display.

    1.  Select the operator default icon that is to the left of the operator name.

    2.  Select <span class="SAP-icons"></span> \(Operator icon/image\).

        The *Upload Operator Icon* dialog box opens.

    3.  Select one of the following options based on the location of the icon file:

        -   Select *From icon list* and choose an icon from the list.
        -   Select *Upload SVG* and select <span class="SAP-icons"></span> \(Upload File\).

    4.  Select *OK*.

        The application uses the new icon for the operator on the graph editor.

        > ### Note:  
        > The size of the icon tile in the operator editor is `80 px` x `80 px`. To ensure that the uploaded SVG file fits within the icon tile, define the `viewbox` property for the SVG file accordingly.


8.  **Optional:** Upload auxiliary files.

    You can upload auxiliary files to the repository that the operator can access or execute at runtime. This file can be any type, for example, binary executables such as a JAR file that the application must execute when executing the operator.

    1.  In the operator editor toolbar, choose <span class="SAP-icons"></span> \(Upload Auxiliary File\).

        These files are stored along with the operators in the operator directory. You can access these files from the SAP Data Intelligence System Management application. Alternatively, you can also upload files from the *Repository* tab.


9.  **Optional:** Select *JSON* in the upper right of the Modeler.

    The JSON file opens showing the parameters for the new operator.


**Related Information**  


[Creating Configuration Types](../creating-configuration-types-2e63e4c.md "Configuration types are JSON files that allow you to define properties and bind them with data types. You can also associate the properties with certain validations, define its UI behavior, and more.")

[Creating Configuration Types](../creating-configuration-types-2e63e4c.md "Configuration types are JSON files that allow you to define properties and bind them with data types. You can also associate the properties with certain validations, define its UI behavior, and more.")

