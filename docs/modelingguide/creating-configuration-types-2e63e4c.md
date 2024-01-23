<!-- loio2e63e4cb102d4459abffa13ff5ef15dc -->

<link rel="stylesheet" type="text/css" href="css/sap-icons.css"/>

# Creating Configuration Types

Configuration types are JSON files that allow you to define properties and bind them with data types. You can also associate the properties with certain validations, define its UI behavior, and more.



## Context

Configuration types are based on JSON schema, but you can create them in the SAP Data Intelligence Modeler application. Reuse your configuration types, for example, in the type definition to define the operator configurations or of specific parameters within the operator configuration definition.

The Modeler also provides global configuration types, which are associated with the configuration parameters of certain default operators \(base operators\) available within the application. To create a new configuration type, perform the following steps in the Modeler application:



## Procedure

1.  Open the *Configuration Types* tab in the navigation pane.

2.  Choose :heavy_plus_sign: in the navigation pane toolbar.

3.  **Optional:** Type a helpful description for the new configuration type in the *Description* text field.

4.  Choose :heavy_plus_sign: in the *Properties* pane.

    Configuration types can have more than one property.

5.  Type a name and display name for the property, and optionally enter a description.

    The application uses the value in the *Title* as the display name for the property in the UI.

    > ### Note:  
    > If you don’t provide a *Title*, then the application uses the value in the *Name* text field as the display name.

6.  Select the required data type value from the *Type* list based on the descriptions in the following table.


    <table>
    <tr>
    <th valign="top">

    Value
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    String
    
    </td>
    <td valign="top">
    
    Define helpers for properties of data type string. Helpers allow you to identify the property type and define values accordingly. Complete the following properties as helpers:

    -   *Format*: Select the applicable format.

        > ### Note:  
        > Applicable only when you select *Auto* for *UI Control*. The Modeler supports the formats, Datetime, Email, URL, Password, or com.sap.dh.connection.id for properties of data type string.

    -   *Value Help*: Select one of the following values:

        Pre-defined Values: Preconfigure the property with a list of values that your users can choose from the user interface. The Modeler displays the property as a dropdown list of values. When you select Pre-defined Values, you must also provide a list of values in the *Values* text field.

        Value from Service: Specify a URL to obtain the property values from the REST API. The application displays the response from the service call as auto-suggestions to users. In the *Url* text field, specify the service URL. The response from the REST API can be an array of strings or an array of objects. If the response is an array of objects, in the *Value path* field, provide the name of an object property. The application renders the values of this object property in a dropdown list in the UI to define the operator configuration. If the response is object, in the *Data path* field, provide the name of an object property.

        > ### Restriction:  
        > The URL should be of the same origin. Cross-origin requests aren’t supported.



    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Object
    
    </td>
    <td valign="top">
    
    For properties of data type object, the application lets specify the schema of the object by drilling down into the object definition. In the *Properties* section, double-click the property to drilldown further and define the object schema.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Array
    
    </td>
    <td valign="top">
    
    For properties of data type array, you can specify the data types of items in the array. In the *Item Type* dropdown list, select a value. The application supports string, number, object, and custom as data types for array items.

    If the *Item Type* is *Object*, in the *Properties* section, double-click the property to drilldown further and define the object schema.

    If the *Item Type* is *Custom*, select and reuse any of the predefined types for the property definition.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Number
    
    </td>
    <td valign="top">
    
    For properties of data type number, you can provide numbered values to the property.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Boolean
    
    </td>
    <td valign="top">
    
    For properties of data type Boolean, you can provide Boolean values to the property.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Integer
    
    </td>
    <td valign="top">
    
    For properties of data type integer, you can provide integer values to the property.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Custom Type
    
    </td>
    <td valign="top">
    
    Custom data types enable you to set the data type of a property to another user-defined type. In the *Type* dropdown list, select a value. The application populates the dropdown list with the global schema types.
    
    </td>
    </tr>
    </table>
    
7.  **Optional:** Set the *Required* toggle to true \(on\).

    When on, users must provide values to the property in the user interface. The property value can’t be empty.

8.  **Optional:** Set *ReadOnly* to true \(on\).

    Applicable for certain types. When on, the Modeler doesn’t allow any edits to the property from the user interface.

9.  **Optional:** Control property visibility by selecting one of the following options:

    -   *Visible*: All properties are visible in the user interface.
    -   *Hidden*: Some properties are visible in the user interface.
    -   *Conditional*: Properties are visible in the user interface based on set conditions. The application performs AND operation of all conditions to determine whether the property is visible or hidden.

10. Create additional properties as necessary.

11. Choose :floppy_disk: and enter a name that includes the fully qualified path to the new configuration type.

    For example, `com.sap.others.<typename>`.

    The Modeler stores the configuration type in a folder structure in the repository.

12. **Optional:** To save another instance of the configuration type, choose :floppy_disk: and enter a different name with the fully qualified path.


**Related Information**  


[Creating Operators](using-operators/creating-operators-049d2f3.md "Use the SAP Data Intelligence Modeler to create your own operators to use in graphs (pipelines).")

