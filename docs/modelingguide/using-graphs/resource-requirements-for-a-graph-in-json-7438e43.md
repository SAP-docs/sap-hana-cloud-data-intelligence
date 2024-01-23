<!-- loio7438e4344c98464dad257c8275e55586 -->

# Resource Requirements for a Graph in JSON

View and overwrite resource requirements in the JSON file of a graph.

Resource requirements are specified in the `graph.json` file. The `groupResources` property provides the default resource requirements for all groups. For a group \(except `default`\), you can overwrite requirements in `resources` property in the group definition.

> ### Example:  
> Here is an example of a modified data generator demo graph \(unnecessary details are omitted\):
> 
> > ### Sample Code:  
> > ```
> > {
> >    "groupResources": {
> >        "requests": {
> >            "cpu": "0.5",
> >            "memory": "4M"
> >        },
> >        "limits": {
> >            "cpu": "1.5",
> >            "memory": "16M"
> >        }
> >    },
> >    "description": "Data Generator",
> >    "processes": {
> >        "datagenerator1": {
> >            "component": "com.sap.util.dataGenerator",
> >            ...
> >        },
> >        "1mnu": {
> >            "component": "com.sap.util.terminal",
> >            ...
> >        }
> >    },
> >    "groups": [
> >        {
> >            "name": "group1",
> >            "nodes": [
> >                "datagenerator1"
> >            ],
> >            "resources": {
> >                "requests": {
> >                     "cpu": "1",    
> >        },
> >        "limits": {
> >            "cpu": "2",
> >            "memory": "32M"
> >                }
> >            }
> >        }
> >    ],
> >    "connections": [
> >        {
> >            "src": {
> >                "port": "output",
> >                "process": "datagenerator1"
> >            },
> >            "tgt": {
> >                "port": "in1",
> >                "process": "1mnu"
> >            }
> >        }
> >    ]
> > }
> > ```
> 
> In this example graph, there are two groups: `default` \(contains `terminal` operator\) and `group1` \(contains `dataGenerator` operator\). Resource requirements from groupResources are applied to the `default` group:
> 
> > ### Sample Code:  
> > ```
> > {
> >     "groupResources": {
> >         "requests": {
> >             "cpu": "0.5",
> >             "memory": "4M"
> >         },
> >         "limits": {
> >             "cpu": "1.5",
> >             "memory": "16M"
> >         }
> >     },
> >     ...
> > }
> > ```
> 
> First the resource requirements from the `groupResources` property is applied to `group1`. Then all resource requirements are overwritten for `group1` but not `memory request` \(because it's not specified for `group1`\):
> 
> > ### Sample Code:  
> > ```
> > {
> >   ...
> >     "groups": [
> >         {
> >             "name": "group1",
> >             "resources": {
> >                  "requests": {
> >                     "cpu": "1"
> >                 },
> >                "limits": {
> >                     "cpu": "2",
> >                     "memory": "32M"
> >                 }
> >             }
> >         }
> >     ],
> >   ...
> > }
> > ```

**Parent topic:**[Maintain Resource Requirements for Graphs](maintain-resource-requirements-for-graphs-44ad625.md "Specify compute resource requirements, such as CPU and memory limits, for graph groups in SAP Data Intelligence Modeler.")

**Related Information**  


[Configure Resources for a Graph](configure-resources-for-a-graph-b0a5a31.md "You can add and specify resource configuration for a graph or the groups within the graph.")

