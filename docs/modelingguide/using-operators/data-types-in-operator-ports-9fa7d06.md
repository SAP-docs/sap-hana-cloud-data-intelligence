<!-- loio9fa7d06c394a451fa515a94b8c6123d8 -->

# Data Types in Operator Ports

Before you choose a data type for a new port, consider the type of connection and what the downstream or upstream operator accepts.



<a name="loio9fa7d06c394a451fa515a94b8c6123d8__section_p2g_4j3_rvb"/>

## Data Type of None

In addition to the other data types of Global, Local, and Dynamic, you can also select None when you add a port to an operator. The None data type indicates a message with headers and no body. The None data type is meant for transmitting metadata and not data.



<a name="loio9fa7d06c394a451fa515a94b8c6123d8__section_hvf_rj3_rvb"/>

## Any Port Type

The Modeler has provided port types that have input and output ports without any defined Data Type and Data Type ID. We call this type of port “any”. When you view the port details for the Terminal, Wiretap, and Graph Terminator operators, the *Data Type* and the *Data Type ID* options have an asterisk \(\*\) as a value.

The Modeler doesn't allow you to create an “any” port type.



<a name="loio9fa7d06c394a451fa515a94b8c6123d8__section_izq_hk3_rvb"/>

## Port Compatibility

The Modeler allows only certain types of ports to connect. The target port has to be at least as general as the source port.

A port with a defined Type ID can't receive a Dynamic type.

> ### Note:  
> A port with a Dynamic scope has an asterisk \(\*\) as the *Data Type ID*. Dynamic ports are created during runtime and exist only in memory.

The Modeler doesn't allow you to connect ports that have specific Data Type IDs. If you ever require connecting incompatible port types, SAP recommends that you implement a custom solution with a script operator to receive data as one type and send it as another data type.

The following table lists characteristics of an output port with the compatible port characteristics of the input port.


<table>
<tr>
<th valign="top">

Output port

</th>
<th valign="top">

Compatible input port

</th>
</tr>
<tr>
<td valign="top">

Port type: Dynamic

Data Type ID: Any

</td>
<td valign="top">

Data Type ID: Any

</td>
</tr>
<tr>
<td valign="top">

Data Type ID: Any

</td>
<td valign="top">

Port type: Dynamic

Data Type ID: Any

</td>
</tr>
<tr>
<td valign="top">

Port type: Dynamic

Data Type ID: Any

</td>
<td valign="top">

Data Type ID: Any

</td>
</tr>
<tr>
<td valign="top">

Port type: None

</td>
<td valign="top">

Data Type ID: Any

</td>
</tr>
<tr>
<td valign="top">

Port type: None

</td>
<td valign="top">

Port type: Dynamic

Data Type ID: Any

</td>
</tr>
<tr>
<td valign="top">

Data Type ID: Any

</td>
<td valign="top">

Port type: Dynamic

Data Type ID: Any

</td>
</tr>
<tr>
<td valign="top">

Port type: Dynamic

</td>
<td valign="top">

Port type: Dynamic

</td>
</tr>
</table>

Keep in mind that, in all cases with dynamic port type, the data type of the connected ports have to match.

> ### Example:  
> You can connect an operator with a table type port and a dynamic scope to one of the following table ports: any, none, or dynamic.

