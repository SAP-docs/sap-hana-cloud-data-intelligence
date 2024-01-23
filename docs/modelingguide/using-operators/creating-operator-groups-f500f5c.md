<!-- loiof500f5ceaed34bcc8fede101edc0604e -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Creating Operator Groups

Partition a graph into subgroups so that each subgroup runs in a different Docker container assigned to different cluster nodes.



<a name="loiof500f5ceaed34bcc8fede101edc0604e__prereq_rgb_hdl_pvb"/>

## Prerequisites

Before you perform the following task, open the applicable graph \(pipeline\) in which to create operator groups.

For complete information about creating and using operator groups, see [Groups, Tags, and Dockerfiles](../using-graphs/groups-tags-and-dockerfiles-03d1ef5.md).



## Context

An operator group can consist of one or many operators. Like individual operators, each group, called a subgraph, is associated with configuration parameters. Provide custom values for the parameters, and define additional configuration parameters for the group.

To create operator groups \(subgraphs\), open SAP Data Intelligence Modeler and perform the following steps in the applicable graph:



## Procedure

1.  Press the [Shift\] key and select each operator to include in the operator group.

2.  Right-click and choose *Group*.

    The Modeler shows the subgraph in a shaded box.

3.  Select <span class="SAP-icons"></span> \(Show Configuration\) in the editor bar.

    The Modeler lists the predefined configuration parameters applicable for the group. The following table describes the parameters that you can define with custom values.


    <table>
    <tr>
    <th valign="top">

    Parameter
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    *Description*
    
    </td>
    <td valign="top">
    
    Provides a description for the operator group.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Restart Policy*
    
    </td>
    <td valign="top">
    
    Determines the behavior of the cluster scheduler when a group execution results in a crash. Choose a value from the list. If you don't select a value, the Modeler uses the default value of *never*:

    -   *never*: The cluster scheduler doesn't restart the crashed group and the crash results in the final state of the graph as “dead”.
    -   *restart*: The cluster scheduler restarts the group execution. The restart changes the state of the graph from dead to pending and then to running.

        > ### Caution:  
        > When you restart a group, a single message per inbound connection can be lost.



    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Tags*
    
    </td>
    <td valign="top">
    
    Describes the runtime requirement of groups. To define tags for the group, select :heavy_plus_sign:and select the required tag and version.

    You can assign more than one tag to a group.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Multiplicity*
    
    </td>
    <td valign="top">
    
    Determines the number of executions for this group at runtime.

    Specify the value as an integer. For example, set to 3 to have the Modeler execute 3 instances of this group at runtime.

    When the Multiplicity is set to greater than 1, the Modeler sends the data arriving at the group in a round-robin fashion.
    
    </td>
    </tr>
    </table>
    
4.  **Optional:** To define new configuration parameters for the group, select :heavy_plus_sign:

    1.  Enter a name for the property in the *Add Property* dialog box.

    2.  Select the property type.

        Select Text, JSON, or Boolean based on whether the property value is a string, JSON, or Boolean value.

    3.  Enter a value in *Value*.

    4.  Select *OK*.



