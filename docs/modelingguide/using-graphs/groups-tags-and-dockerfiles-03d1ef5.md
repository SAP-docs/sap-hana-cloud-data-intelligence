<!-- loio03d1ef5a40d8426d9e92ec0d3e469df5 -->

# Groups, Tags, and Dockerfiles

Groups, tags, and Dockerfiles are essential parts of the SAP Data Intelligence environment for running graphs \(pipelines\) more efficiently. Therefore, you must understand how they work together.



## Groups

A group is an aggregation of operators in a graph that have similar technical requirements or that run in a common Docker image. When you run a graph with groups, each group runs in a different Docker container. Each Docker container has the possibility of having a different Docker image. The Modeler selects a group's Docker image automatically based on the tags associated with the image. The operators in a group run in the same node. You can configure each group with a different restart policy, tags, or multiplicity.

> ### Example:  
> Assign different restart policies for each group in a graph:
> 
> -   Group 1 has a restart policy where the container redeploys when the group fails.
> -   Group 2 has a restart policy where the graph terminates when the group fails.

The most common reason for using groups is to distribute work among many compute nodes. Distribute work by partitioning the graph into many groups and \(or\) adding multiplicity larger than 1 for a group. Distributing work among many compute nodes can result in better graph throughput and cluster utilization.

> ### Note:  
> Multiplicity determines the number of runs for the group at runtime.

If there's no Dockerfile that satisfies the requirements of a graph, you can partition a graph into groups in such a way that, for each group, there exists at least one Dockerfile that satisfies the graph's requirements.

A graph with no group defined explicitly has only one group, the default group. A default group contains all operators from the graph that haven't been assigned to an explicit group. You can partition the graph by assigning a subset of operators to an explicit group.

> ### Example:  
> You have a non-partitioned graph with the following topology: A → B → C → D → E. All operators in this graph run in the default group.
> 
> You decide to create 2 explicit groups:
> 
> -   Group 1 contains A and B
> -   Group 2 contains E
> 
> When you include the default group, your graph now has 3 groups:
> 
> -   Group 1: \(A → B\)
> -   Group 2: \(E\)
> -   Default group: C → D
> 
> The resulting topology is as follows: \(A → B\) → C → D → \(E\).



<a name="loio03d1ef5a40d8426d9e92ec0d3e469df5__section_ldz_hrn_cxb"/>

## Tags and Dockerfiles

When running a graph, the Modeler selects a Docker image for each group based on the group's tags. View the available tags in the *Tags* list in the group properties. If multiple Dockerfiles meet the tag requirements, the Modeler chooses the Dockerfile with the fewest tags. If the Docker image isn't already cached, the Modeler builds the selected Dockerfile during the graph run.

Each tag represents a software component, such as a package or library, that is required at runtime for a group. The Modeler identifies the software component by a pair of values in the following format:

```
{
"<resource_id>":"<resource_version>"
}
```

.

> ### Example:  
> The following are examples of value pairs for software component:
> 
> ```
> {
> "python":"3.9"
> }
> 
> ```
> 
> ```
> {
> "tornado":"6.1.0"
> }
> ```
> 
> ```
> {
> "opencv":""
> }
> ```
> 
> > ### Note:  
> > An empty <code><i class="varname">&lt;resource_version&gt;</i></code>, such as `""`, means that the Modeler can use any version of the component.

The final list of tags for a group is a combination of the following:

-   individual tags specified by each operator
-   tags from the group configuration

When determining the final list of tags, the Modeler searches for a Dockerfile in your repository directory that meets all requirements. If two operators in the same group require the same resource but different versions, and the versions are compatible, the Modeler uses the more specific version. If the versions aren't compatible, the Modeler issues an error.

> ### Example:  
> If one operator requires version <code>“1.1”</code> of component <code>“foo”</code> and another operator requires version <code>“1.1.2”</code>, the Modeler selects version <code>“1.1.2”</code> because it's more specific. However, if one operator requires version <code>“1.1”</code> and the other requires <code>“2.1.1”</code>, the Modeler issues an error because versions <code>“1.1”</code> and <code>“2.1.1”</code> don't share a common prefix and aren't compatible.

When the Modeler searches for Dockerfiles that meet a group's tag requirements, it's essential that it determines whether a specific group tag is fulfilled by a Dockerfile tag. A group is considered satisfied by a Dockerfile tag only when the following conditions are met:

-   The resource IDs in both tags are identical.
-   The resource versions share a common prefix.
-   The resource version of the Dockerfile tag is more specific than the resource version of the group tag.

> ### Example:  
> The group tag <code>{“foo”:“1.1”}</code> is satisfied by the Dockerfile tags <code>{“foo”:“1.1”}</code> or <code>{“foo”:“1.1.2”}</code>, but not by <code>{“foo”:“1”}</code>, <code>{“foo”:“”}</code>, or <code>{“bar”:“1.1”}</code>.

If multiple Dockerfiles meet a group's tag requirements, the Modeler doesn't use the specific resource versions defined in each Dockerfile to break the tie; it selects the Dockerfile arbitrarily.

To determine the selected Dockerfile for a group, download the graph diagnostics archive and examine the `image` field in the topic [execution.json File](execution-json-file-8b01d80.md). If no Dockerfile meets a group's needs, the Modeler issues an error. To fix the error, you can either split the group into smaller groups that match existing Dockerfiles or create a new Dockerfile that meets all the group's requirements. For information about creating Dockerfiles, see the topic [Creating Dockerfiles](../creating-dockerfiles/creating-dockerfiles-62d1df0.md).



<a name="loio03d1ef5a40d8426d9e92ec0d3e469df5__section_k2q_24h_hxb"/>

## Default and Deprecated Tags



### Default Tag

The Modeler gives higher priority over other Dockerfiles to the Dockerfiles that have the <code>{“default”:}</code> tag.

> ### Example:  
> A Docker image named `com.sap.sles.base` has the <code>{“default”:}</code> tag and meets the tag requirements. The Modeler chooses the `com.sap.sles.base` Docker image even when other Dockerfiles meet the requirements and have fewer matching tags, because the other Dockerfiles don't have the <code>{“default”:}</code> tag.
> 
> If two Dockerfiles have the <code>{“default”:}</code> tag and meet the tag requirements, the Modeler selects the Dockerfile with the fewer tags.



### Deprecated Tag

Dockerfiles with the <code>{“deprecated”:}</code> tag have a lower priority than other tags.

> ### Example:  
> If the Docker image `com.sap.opensuse.going.zypper` has the <code>{“deprecated”:}</code> tag and meets the tag requirements, the Modeler doesn't choose it over a non-deprecated image, even when it has fewer matching tags.
> 
> If the Modeler has to choose between two Dockerfiles, each with the <code>{“deprecated”:}</code> tag, it chooses the Dockerfile with the fewer matching tags.



<a name="loio03d1ef5a40d8426d9e92ec0d3e469df5__section_dly_c2m_2xb"/>

## Operator Tags

View or edit an operator's tags in the operator editor. Open the editor by right-clicking the operator and choosing *Edit*.

The operators that run on subengines can have implicit tags. Implicit tags don't appear on the operator editor screen; they're included in the requirements of a group using the operator. Check each subengine's documentation for more information about its implicit tags. The following table lists the implicit tags for all active subengines.


<table>
<tr>
<th valign="top">

Subengine

</th>
<th valign="top">

Implicit Tags

</th>
</tr>
<tr>
<td valign="top">

ABAP

</td>
<td valign="top">

vrep \(runs using any image\)

</td>
</tr>
<tr>
<td valign="top">

Node.js

</td>
<td valign="top">

node

</td>
</tr>
<tr>
<td valign="top">

Python 3.9

</td>
<td valign="top">

-   'tornado':'6.1.0'
-   'sles':""
-   'python':'3.9'



</td>
</tr>
<tr>
<td valign="top">

C++

</td>
<td valign="top">

Deprecated

</td>
</tr>
</table>

> ### Caution:  
> Be careful when you add or change tags for existing operators or groups. Tags affect the selection of the Docker image. Modifying tags can alter the Dockerfile that the Modeler chooses during graph execution, which can cause unexpected results or errors. SAP recommends that you thoroughly review the tag changes and the impact on the Docker image selection process before you complete any modifications.

The following example shows how tags affect the selection of Docker images and the Dockerfile that the Modeler chooses during graph execution.

> ### Example:  
> Your repository has the following Dockerfiles and associated tags:
> 
> -   **com.sap.d1:** <code>{“python36”:“”, “pandas”:“1.2.3”, “numpy36”:“”, “tornado”:“1.1.1”, “pyarrow”:“”}</code>
> -   **com.sap.d2:** <code>{“python36”:“” , “corge”:“2.2.2”}</code>
> -   **com.sap.d3:** <code>{“node”:“”}</code>
> 
> The tags associated with a group in a graph are the union of each operator's tags and the tags specified in the group configuration.
> 
> A graph with the topology of \(A→B→C\)→D→E, has the following groups:
> 
> -   **Explicit group:** \(A, B, C\)
> -   **Default group:** \(D, E\)
> 
> The following table lists the group configurations and operators with their corresponding associated tags.
> 
> 
> <table>
> <tr>
> <th valign="top">
> 
> Group Configuration or Operator
> 
> </th>
> <th valign="top">
> 
> Associated Tags
> 
> </th>
> </tr>
> <tr>
> <td valign="top">
> 
> Explicit group configuration
> 
> </td>
> <td valign="top">
> 
> <code>{“python36”:“”, “pandas”:“”}</code>
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Default group configuration
> 
> </td>
> <td valign="top">
> 
> `{ }`
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Operator A
> 
> </td>
> <td valign="top">
> 
> <code>{“numpy36”:“”}</code>
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Operator B
> 
> </td>
> <td valign="top">
> 
> <code>{“pandas”:“1.2”, “tornado”:“1.1.1”}</code>
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Operator C
> 
> </td>
> <td valign="top">
> 
> `{ }`
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Operator D
> 
> </td>
> <td valign="top">
> 
> `{ }`
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> Operator E
> 
> </td>
> <td valign="top">
> 
> <code>{“python36”:“”}</code>
> 
> </td>
> </tr>
> </table>
> 
> The following are the results when you associate the union of the tags with each group results:
> 
> -   **Explicit group \(A, B, C\):** <code>{“python36”:“”, “pandas”:“1.2”, “numpy36”:“”, “tornado”:“1.1.1”}</code>
> -   **Default group \(D, E\):** <code>{“python36”:“”}</code>
> 
> The Modeler determines a Dockerfile for each group using the following information:
> 
> -   The aggregation of the tags in the **Explicit group** are satisfied only by the Dockerfile **com.sap.d1**.
>     -   The Dockerfile **com.sap.d1** has one more tag <code>{“pyarrow”:“”)</code> than **Group 1** requires.
> 
> -   The <code>“1.2.3”</code> version for <code>“pandas”</code> in **com.sap.d1** satisfies the **Explicit group**.
>     -   The **Explicit group** requires version <code>“1.2”</code>, but <code>“1.2.3”</code> is more specific.
> 
> -   The **Default group** has two Dockerfiles that satisfy the aggregated tags: **com.sap.d1** and **com.sap.d2**.
> 
> The Modeler chooses the Dockerfiles with fewer tags:
> 
> -   `com.sap.d1` for Explicit group
> -   `com.sap.d2` for Default group

