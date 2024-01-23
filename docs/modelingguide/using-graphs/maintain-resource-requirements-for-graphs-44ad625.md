<!-- loio44ad62548b3a41fc81b16f42031038a8 -->

# Maintain Resource Requirements for Graphs

Specify compute resource requirements, such as CPU and memory limits, for graph groups in SAP Data Intelligence Modeler.

For each resource type, specify CPU and memory limits in the *Requests* and *Limits* properties of the *Configuration* pane.

-   The *Requests* properties specify the initial resource quantities for memory and CPU that the Modeler requires to start the graph group execution. If the resource availability isn't enough, then the graph execution fails to start. Default settings are as follows:
    -   Memory: 256 Mebibytes \(Mi\)
    -   CPU: 0.3 CPU

-   The *Limits* properties specify the limits for resource usage for memory and cpu. If the graph group execution violates the limit set for memory, the Modeler terminates the graph execution. If the graph group execution uses excessive CPU, the set CPU limit helps control the CPU consumption by the graph group. Default settings are as follows:
    -   Memory: 3 Gibibytes \(Gi\)
    -   CPU: 3 CPU


If you don't specify memory and CPU limits in the *Resources* section of the *Configuration* pane, the Modeler uses the default limits.

When you set resources for *Requests* and *Limits* in the *Configuration* pane, you also select the resource units. SAP uses the same notations as Kubernetes to specify the resource quantity. For more information on memory and CPU resource units, see the following Kubernetes documentation:

-   [Memory resource units](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory) 
-   [CPU resource units](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-cpu) 

For more information about CPU and memory size considerations, see [Sizing for Data Pipelines](https://help.sap.com/docs/SAP_DATA_INTELLIGENCE/ea95bb6d8ac24cd6a4ad396ca5e35bc6/c7bd6c8a19014e75a319fab59e1b4a98.html?state=LATEST&version=Cloud) in the *Sizing Guide for Cloud*.



<a name="loio44ad62548b3a41fc81b16f42031038a8__section_kb2_h5g_cvb"/>

## Errors and Warnings

When a graph or graph group exceeds the limits you set in *Resources*, the Modeler issues an error and the graph doesn't run.

If you don't set limits in *Resources*, the Modeler uses the default limits and issues a warning or an error. The message instructs you to adjust the CPU and memory limits for the graph. The following lists when the Modeler issues a warning or an error:

-   **Warning:** When you save or run a graph, and the Modeler validates the graph \(implicit validation\), the Modeler issues a warning.
-   **Error:** When you validate the graph manually \(explicit validation\), the Modeler issues an error.

Adjust the limits either in the Modeler or in the `graph.json` file.

-   **[Resource Requirements for a Graph in JSON](resource-requirements-for-a-graph-in-json-7438e43.md "View and overwrite resource requirements in the JSON file of a graph.")**  
View and overwrite resource requirements in the JSON file of a graph.
-   **[Configure Resources for a Graph](configure-resources-for-a-graph-b0a5a31.md "You can add and specify resource configuration for a graph or the groups within the graph.")**  
You can add and specify resource configuration for a graph or the groups within the graph.

