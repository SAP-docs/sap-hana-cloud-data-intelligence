<!-- loio4fd1229c9bee4ce88036b641e7e7c434 -->

# Jupyter Operator Predefined Functions

There are functions available from the Jupyter notebook that you can use in SAP Data Intelligence and the Jupyter operator.

You can access the documentation of a function at any time inside the Jupyter notebook user interface:

-   Short description: press [Shift-Tab\] on top of the function name \(inside a code cell\).
-   Complete description: [Shift-Tab-Tab\] on top of the function name \(inside a code cell\).



<a name="loio4fd1229c9bee4ce88036b641e7e7c434__section_u4j_g55_zyb"/>

## api.send\(port, data\)

This function writes the data to the specified operator output port. Be careful with the correspondence between the Python data object and the Modeler port type.

**Arguments**


<table>
<tr>
<td valign="top">

`port (str)`

</td>
<td valign="top">

Operator output port name.

</td>
</tr>
<tr>
<td valign="top">

`data`

</td>
<td valign="top">

Data object to send.

</td>
</tr>
</table>



<a name="loio4fd1229c9bee4ce88036b641e7e7c434__section_r4c_355_zyb"/>

## api.get\_config\(\)

This function returns the Jupyter operator's configuration object.



### Arguments

None



### Returns

`config(dict)`: configuration object.



<a name="loio4fd1229c9bee4ce88036b641e7e7c434__section_ltx_j55_zyb"/>

## api.add\_dependency\(package\_name\)

This function attempts to install a Python package using pip. If the installation fails, the application raises an exception.



### Arguments

`package_name (str)`: the name of the package to be installed with pip.



<a name="loio4fd1229c9bee4ce88036b641e7e7c434__section_ar3_n55_zyb"/>

## api.try\_port\_callback\(ports, callback\)

Runs the callback once with the data retrieved from the specified input ports. The callback is called only when there are messages available in all input ports.

> ### Note:  
> This function is available only in interactive mode.

**Arguments**


<table>
<tr>
<td valign="top">

`ports (str|list[str])`

</td>
<td valign="top">

Input ports to be tested with the callback. \`ports\` can be one of the following:

-   A list of strings with the name of each port to be associated.
-   A string to associate the callback with a single port.



</td>
</tr>
<tr>
<td valign="top">

`callback (func[...])`

</td>
<td valign="top">

A callback function with the same number of arguments as elements in \`ports\`.

The arguments are passed to \`callback\` in the same order as their corresponding ports in the \`ports\` argument.

</td>
</tr>
</table>



<a name="loio4fd1229c9bee4ce88036b641e7e7c434__section_skk_r55_zyb"/>

## api.set\_port\_callback\(ports, callback\)

This function associates the input ports with the callback. The callback is called only when there are messages available in all input ports. If this function is called multiple times for the same group of ports, then the previous callback is overwritten by the provided one.

> ### Note:  
> Different ports group can't overlap. For example, a port can be only associated with one callback at a time.

**Arguments**


<table>
<tr>
<td valign="top">

`ports (str|list[str])`

</td>
<td valign="top">

Input ports to be associated with the callback. \`ports\` can be one of the following:

-   A list of strings with the name of each port to be associated.
-   A string to associate the callback with a single port.



</td>
</tr>
<tr>
<td valign="top">

`callback (func[...])`

</td>
<td valign="top">

A callback function with the same number of arguments as elements in \`ports\` or a variable-length argument.

The arguments are passed to \`callback\` in the same order as their corresponding ports in the \`ports\` argument.

</td>
</tr>
</table>



<a name="loio4fd1229c9bee4ce88036b641e7e7c434__section_imv_t55_zyb"/>

## api.remove\_port\_callback\(callback\)

This function unregisters the callback function. If the function isn't registered, the method exits quietly.



### Arguments

`callback (func[...])`: callback function to be removed.

