<!-- loio72d5fa178d804ac9a56f0295814c5bd2 -->

# Graph Validation Warnings and Errors

When a graph validation isn't successful, the Data Intelligence Modeler creates a list of warnings and errors, with a link to additional information about the warning or error.

The following table describes some of the warnings and errors from a graph validation.

****


<table>
<tr>
<th valign="top">

Message

</th>
<th valign="top">

Component

</th>
<th valign="top">

Severity

</th>
<th valign="top">

Quick Fix

</th>
</tr>
<tr>
<td valign="top">

There are no operators in the graph.

</td>
<td valign="top">

isGraphEmpty

</td>
<td valign="top">

Warning

</td>
<td valign="top">

Add operators to the graph.

</td>
</tr>
<tr>
<td valign="top">

Invalid graph description. Special characters are not allowed.

</td>
<td valign="top">

Validate Graph Description

</td>
<td valign="top">

Error

</td>
<td valign="top">

Check `graph.json` for special characters in the description.

</td>
</tr>
<tr>
<td valign="top">

Group name is either missing or not unique.

</td>
<td valign="top">

Validate Single Group

</td>
<td valign="top">

Error

</td>
<td valign="top">

Check `graph.json` to add missing group names, and modify identical group names.

</td>
</tr>
<tr>
<td valign="top">

The `tagdatabase` of graph <code><i class="varname">&lt;graph_name&gt;</i></code> is empty.

</td>
<td valign="top">

Check tags

</td>
<td valign="top">

Error

</td>
<td valign="top">

Check your repository or `Tags.json` files for errors. Errors occur in the <code><i class="varname">&lt;graph_name&gt;</i></code> file.

</td>
</tr>
<tr>
<td valign="top">

Matching Dockerfile couldn't be found.

</td>
<td valign="top">

Check tags

</td>
<td valign="top">

Error

</td>
<td valign="top">

Check your repository `Tags.json` files, or other resources, for errors. Also check for missing or incorrect tags in the group configuration.

</td>
</tr>
<tr>
<td valign="top">

The graph <code><i class="varname">&lt;graph_name&gt;</i></code> has a single operator.

</td>
<td valign="top">

Check Operator Connections

</td>
<td valign="top">

Warning

</td>
<td valign="top">

This graph can execute with current configuration. However, consider adding more operators to the graph based on your requirement.

</td>
</tr>
<tr>
<td valign="top">

Incompatible ports are connected \(source: port %s of operator %s, target: port %s of operator %s\).

</td>
<td valign="top">

Check Connection Types

</td>
<td valign="top">

Error

</td>
<td valign="top">

Provide connection between compatible ports only.

</td>
</tr>
<tr>
<td valign="top">

Operator <code><i class="varname">&lt;operator_name&gt;</i></code> either deprecated or beta.

</td>
<td valign="top">

Validate Operator Versions

</td>
<td valign="top">

Warning

</td>
<td valign="top">

This graph can execute with current configuration. However, consider using nondeprecated or nonbeta operators.

</td>
</tr>
<tr>
<td valign="top">

Operator <code><i class="varname">&lt;operator_name&gt;</i></code> does not exist in the registry.

</td>
<td valign="top">

Validate Port Names

</td>
<td valign="top">

Warning

</td>
<td valign="top">

Check that the operator <code><i class="varname">&lt;operator_name&gt;</i></code> is correct and saved sucessfully.

</td>
</tr>
<tr>
<td valign="top">

Some groups are missing resource definitions. If the resource request is missing and the limit is set, the request shall use the smaller value from either the limit set or the default request value.

</td>
<td valign="top">

Validate Graph Resources

</td>
<td valign="top">

Error

The message is an error when you validate the graph manually \(explicit validation\).

</td>
<td valign="top">

Without selecting any part of the graph in the canvas:

1.  Open the *Configuration* pane.
2.  Expand *Resources*.
3.  Select the *Edit* icon.
4.  Add or edit the resource limits.

For more information about limits, see [Maintain Resource Requirements for Graphs](maintain-resource-requirements-for-graphs-44ad625.md).

</td>
</tr>
<tr>
<td valign="top">

Some groups are missing resource definitions. If the resource request is missing and the limit is set, the request shall use the smaller value from either the limit set or the default request value.

</td>
<td valign="top">

Validate Graph Resources

</td>
<td valign="top">

Warning

The message is a warning when you save or run a graph, and the Modeler validates the graph \(implicit validation\).

</td>
<td valign="top">

Without selecting any part of the graph in the canvas:

1.  Open the *Configuration* pane.
2.  Expand *Resources*.
3.  Select the *Edit* icon.
4.  Add or edit the resource limits.

For more information about limits, see [Maintain Resource Requirements for Graphs](maintain-resource-requirements-for-graphs-44ad625.md).

</td>
</tr>
<tr>
<td valign="top">

Group restart policy is set to `'restart'` for the following groups, while snapshot is enabled: <code><i class="varname">&lt;group_name&gt;</i></code>.

</td>
<td valign="top">

Validate Restart Policy

</td>
<td valign="top">

Error

</td>
<td valign="top">

Change the restart policy for the following groups: <code><i class="varname">&lt;group_name&gt;</i></code>.

</td>
</tr>
<tr>
<td valign="top">

Operator <code><i class="varname">&lt;operator_name&gt;</i></code> has a manual connection, which might contain sensitive information, such as ID and password.

</td>
<td valign="top">

Validate Manual Connection

</td>
<td valign="top">

Warning

</td>
<td valign="top">

Use a connection from Connection Manager rather than the manual connection.

</td>
</tr>
<tr>
<td valign="top">

Operator <code><i class="varname">&lt;operator_name&gt;</i></code> is using the “propagate to error port” error handling option but its error port is not connected or not present.

</td>
<td valign="top">

Validate Error Handling Ports

</td>
<td valign="top">

Error

</td>
<td valign="top">

Connect the error port of this operator or change its error handling type.

</td>
</tr>
</table>

