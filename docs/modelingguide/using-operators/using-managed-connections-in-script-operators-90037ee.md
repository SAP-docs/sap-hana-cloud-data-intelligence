<!-- loio90037ee27fbc4194bc0b6c5f2d9e3e7b -->

# Using Managed Connections in Script Operators

You can use managed connections in operator configurations of the script operators.



## Context

For this task, we use the Python3 operator as an example.



## Procedure

1.  Create a new Python3 operator.

    For instruction, see [Creating Operators](creating-operators-049d2f3.md).

2.  Add a new configuration parameter for the operator.

3.  Add a new property and switch to *JSON* view.

4.  Add a definition of an object-type parameter.

    Copy and paste the following script in the JSON view:

    > ### Note:  
    > This script is applicable only for the Pytho3 operator. In this example, we use the `OPENAPI` connection type as shown in the connection list. To return different connection types, change the value of the `connectionTypes` parameter in `properties.connection.connectionID.sap_vflow_valuehelp.url`.

    ```
    
    {
      "$schema": "http://json-schema.org/draft-06/schema#",
      "$id": "http://sap.com/vflow/demos.conn.testme.configSchema.json",
      "type": "object",
      "properties": {
        "codelanguage": {
          "type": "string"
        },
        "script": {
          "type": "string"
        },
        "connection": {
          "title": "Connection",
          "type": "object",
          "properties": {
            "configurationType": {
              "title": "Configuration Type",
              "type": "string",
              "enum": [
                " ",
                "Configuration Manager"
              ]
            },
            "connectionID": {
              "title": "Connection ID",
              "type": "string",
              "format": "com.sap.dh.connection.id",
              "sap_vflow_valuehelp": {
                "url": "/app/datahub-app-connection/connections?connectionTypes=OPENAPI",
                "valuepath": "id",
                "displayStyle": "autocomplete"
              },
              "sap_vflow_constraints": {
                "ui_visibility": [
                  {
                    "name": "configurationType",
                    "value": "Configuration Manager"
                  }
                ]
              }
            }
          }
        }
      },
      "required": [
        "connection"
      ]
    }
    
    ```

5.  To use the connection properties, copy and paste the following code in the *Script* tab of the Python3 operator editor.

    > ### Example:  
    > In the following code snippet, the host is read from `managedConnectionProperties`, which is chosen in the operator configuration at design-time.
    > 
    > ```
    > 
    > def t1():
    >     managedConnection = api.config.connection
    >     managedConnectionProperties = managedConnection['connectionProperties']
    >     
    >     host = managedConnectionProperties['host']
    >     output = api.Message( host, {})
    >     api.send("out", output)
    > 
    > api.add_timer("1s", t1)
    > 
    > ```

6.  Include the Python3 operator in a graph, and choose the managed connection.


