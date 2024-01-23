<!-- loiof3caf1668ae54046ad7c3049a576d149 -->

# Parameterize the Graph Run Process

Parameterize the graph run process using parameters that assume different values based on the values passed in each graph run.

When you configure operators and groups in a graph manually during design time, the resulting values are the same for all executions of the graph. But, when you parameterize the graph run process, you can change the results for each run.

Use the following two modes of parameterization through the API:

-   Substitution Parameters
-   Graph Parameters

> ### Note:  
> You can't mix the two types of parameterization in the same graph. A graph, however, can be executed using substitution parameters while another instance of the same graph can use graph parameters.

SAP Data Intelligence restricts both methods to operator configurations and group multiplicity. Therefore, you can change a group's CPU or memory limits only during design time.



<a name="loiof3caf1668ae54046ad7c3049a576d149__section_enz_zp2_bwb"/>

## Substitution Parameters

When you use substitution parameters, set values for the parameters at the following times:

-   At runtime, when you run the graph.
-   At design time, by referencing the value of another configuration from the same operator.

    When you reference the value of another configuration from the same operator, the values must always be strings. The values must be strings even for group multiplicity. The system converts the strings to integers internally.


Define a substitution parameter by providing the value to the configuration in the following format: `${parameter_name}`, where `parameter_name` is the name of the substitution parameter. SAP Data Intelligence handles the substitution parameter value as follows:

-   If the name of the substitution parameter \(`parameter_name`\) matches the name of an operation configuration, then the Modeler uses the configuration value as the substitution parameter value.
-   If the name of the substitution parameter \(`parameter_name`\) doesn't match the name of any configuration parameter of the operator, then you provide the value at runtime.

> ### Example:  
> The operator configuration parameter named “Path” is defined with the value `URL://${name}`. In this example, `{name}` is the substitution parameter. You define the value for “Path” by providing a value to `{name}` at runtime.

> ### Example:  
> The following snippet shows an excerpt of a graph JSON with a substitution parameter in an operator configuration:
> 
> ```
> {
> 	"properties": {},
> 	"description": "",
> 	"processes": {
> 		"httpclient1": {
> 			"component": "com.sap.http.client2",
> 			"metadata": {
> 				"label": "HTTP Client",
> 				"config": {
> 					"getConnection": {
> 						"connectionID": "${TO_BE_SUBSTITUTED_CONNECTIONID}"
> 					},
> 					"retryPeriodInMS": 500
> 				}
> 			}
> 		},
> 		...
> }
> ```
> 
> The following code snippet requests the body of an HTTP request that runs a graph named “testSubs”, and sets a value for the substitution parameter as “TO\_BE\_SUBSTITUTED\_CONNECTIONID”:
> 
> ```
> {
>     "src":"test_substitution",
>     "name":"testSubs",
>     "debug":false,
>     "async":true,
>     "configurationSubstitutions":{
>       "TO_BE_SUBSTITUTED_CONNECTIONID": "TEST_HTTP_CONNECTION"
>     }
> } 
> ```



<a name="loiof3caf1668ae54046ad7c3049a576d149__section_h4v_dr2_bwb"/>

## Graph Parameters

Graph parameters support all JSON types. To support graph parameters, SAP Data Intelligence uses the following attributes:

-   `parameters`: Use as part of the graph description. Lists all the schemas that appear between the brackets \(`${}`\) and includes the JSON type. Default values are optional. This field contains the schemas of each para parameter.
-   `parameterMapping`: Use as part of the graph description. Maps an operator configuration property to a value that contains a graph parameter.
-   An entry to the request body that JSON uses to start a graph. Instead of the `configurationSubstitutions`, you can use `parameters` that support any type.

    > ### Example:  
    > The following code snippet uses integer and boolean:
    > 
    > ```
    > {
    >     "src": "test_parameters",
    >     "name": "testParams",
    >     "parameters": {
    >         "eggs": 100,
    >         "dis": true
    >     }
    > } 
    > ```
    > 
    > Where:
    > 
    > -   `eggs` = integer
    > -   `dis` = boolean


The following example shows the extent of the graph parameter feature and how you can use the graph parameters for operator configurations.

> ### Example:  
> ```
> {
> ...
> "parameters": { // Schemas of the substitution parameters
>     "foobar":{
>         "type": "number",
>         "default": 100 // default value if no value is passed
>     },
>     "foobar2": {
>         "type": "object"
>     },
>     "foobar3": {
>         "type": "number"
>     }
> }
> "processes": {
>     "pythonOperator1": {
>         "configuration": {
>             "other": "value",
>             "baz": "3",
>             "test2": "3",
>             "bazarray": [
>                 {
>                     "baz": 2
>                 }
>             ]
>         }
>     }
> }
> "parameterMapping": { // How the parameters will be introduced into the configurations, we should always refer to the parameters with ${}
>     "processes.pythonOperator1.configuration.baz": "where count < ${foobar}", // overwrite existing baz with string "where count < 3".
>     "processes.pythonOperator1.configuration.test": "${foobar2}", // create configuration that expects any JSON object, not requiring further schema
>     "processes.pythonOperator1.configuration.test2": "${foobar3}", // overwrites 3 with the parameters integer value.
>     "processes.pythonOperator1.configuration.bazrray.0.baz": "${foobar}", // overwrites 2 with the parameter value, keep in my the last structure (baz in this case) must be an object.
>     "processes.pythonOperator1.configuration.test": "foobar2 dummy", // ERROR because the value must contain ${}, and the stringification depends only on the type in the schema. 
> }
> ...
> }
> ```



### Type Validation

SAP Data Intelligence performs type validation on the parameters based on their type definition. An invalid type results in the graph run request to fail with an error code of 400.

The following sample code shows how to parameterize group multiplicities and how SAP Data Intelligence works with the operator configurations.

> ### Example:  
> Only integer and number types are allowed. In `parameterMapping`, the system references each group by its index in the graph groups list.
> 
> ```
> {
>     "processes": {
>         "formatconverter1": {
>             "component": "com.sap.util.formatConverter1",
>             "metadata": {
>                 "config": {
>                 }
>             }
>         }
>     },
>     "groups": [
>         {
>             "name": "group1",
>             "nodes": [
>                 "formatconverter1"
>             ],
>             "metadata": {
>                 "description": "Group"
>             }
>         }
>     ],
>     "parameters": {
>         "foo": {
>             "type": "string"	
>         },
>         "bar": {
>             "type": "number"	
>         }
>     },
>     "parameterMapping": {
>         "processes.formatconverter1.configuration.cfg1": "${foo}",
>         "groups.0.multiplicity": "${bar}"
>     }
> }
> ```



<a name="loiof3caf1668ae54046ad7c3049a576d149__section_btx_2hb_hwb"/>

## Limitations

The request to run a graph fails with error “400 bad request” under the following conditions:

-   Parameters are too large. The default threshold is 5 MB.
-   Graph uses both substitution parameters and graph parameters.
-   Parameters aren't valid according to their schema.

**Parent topic:**[Running Graphs](running-graphs-439d0a0.md "After creating a graph, you can run the graph based on the configuration defined for the graph. The Modeler application runs the operators in the graph as individual processes.")

**Related Information**  


[Automatic Graph Recovery](automatic-graph-recovery-4bf172b.md "Configure any graph to recover from failure automatically, regardless of whether the graph uses Generation 1 or Generation 2 operators.")

[Debug Graphs](debug-graphs-06b0159.md "You can start the graph in debug mode to verify the input and output from each operator during execution and analyze or modify the data passing through a connection.")

[Schedule Graph Executions](schedule-graph-executions-cb46d5f.md "The SAP Data Intelligence Modeler provides capabilities to schedule graph executions.")

