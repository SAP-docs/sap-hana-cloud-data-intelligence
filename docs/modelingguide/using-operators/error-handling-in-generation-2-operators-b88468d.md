<!-- loiob88468d2f3184b9098164cfde2af1d8c -->

# Error Handling in Generation 2 Operators

The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.

Error handling operators, whether generic or graph specific, are usually scripted. Generally, the errors communicated to an error operator are for internal use only.

The following table describes the options for error handling.


<table>
<tr>
<th valign="top">

Option

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

*Terminate on error*

</td>
<td valign="top">

Unexpected exceptions are logged and the graph is terminated.

</td>
</tr>
<tr>
<td valign="top">

*Log and ignore*

</td>
<td valign="top">

Unexpected exceptions are logged and the operator continues to run.

</td>
</tr>
<tr>
<td valign="top">

*Propagate to error port*

</td>
<td valign="top">

Unexpected exceptions are sent to an `error` port that is generated at runtime.

This port is of type structure \(`com.sap.error`\), which contains the following fields:

-   `code`: an error code \(`int32`\) that is local to the operator.
-   `operatorID`: a string with the ID of the operator outputting this error \(for example, `com.sap.system.terminal`\).
-   `processID`: a string with the ID in the graph of the process outputting this error \(for example, `terminal1`\).
-   `text`: a string corresponding to the main error message.
-   `details`: a `table` type, which is composed of the fields `key` and `value` \(both of type `string`\), which can be used to provide further information about the exception.

The operator continues to run.

</td>
</tr>
</table>



<a name="loiob88468d2f3184b9098164cfde2af1d8c__section_dql_3fx_rvb"/>

## Error Output Port

Add an error output port to the operator that outputs to the specific error operator. When you create the port, make sure to include “error” in the name, such as `com.sap.error` or `com.sap.error.details`. Error output ports can be either structure or table types.

