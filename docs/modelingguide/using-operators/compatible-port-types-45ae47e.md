<!-- loio45ae47e451fa4a88abfd48d220c543c9 -->

# Compatible Port Types

You can connect two operators only if the output port of the first operator and the input port of the second operator are compatible.



The engine performs compatibility checks when you run the graph and when the engine loads the graph. If the port types aren't compatible, the engine fails the graph with a corresponding message in the trace.

The engine checks for compatibility in two steps as follows:

1.  For the base types, the engine ensures that one of the following rules is true:
    -   The base types of the operators are identical or
    -   One of the base types is of type **any** and the other base type is one of the compatible types listed in the table in [Ports and Port Types](ports-and-port-types-6789999.md).

2.  The semantic type of one port type is a specialization of the semantic type of the other port type. The semantic type, including the empty one, is a specialization of `*`.

    > ### Note:  
    > Omitting the semantic type or empty semantic type, yields a complete type. This type is different from `<base type>.*`, which is an incomplete type.


The following table shows the compatibility of output and input port types.


<table>
<tr>
<th valign="top">

Output Port Types

</th>
<th valign="top">

Input Port Types

</th>
<th valign="top">

Compatible

</th>
<th valign="top">

Reason

</th>
</tr>
<tr>
<td valign="top">

any

</td>
<td valign="top">

any

</td>
<td valign="top">

yes

</td>
<td valign="top">

Identical base type. No semantic type.

</td>
</tr>
<tr>
<td valign="top">

any

</td>
<td valign="top">

any.\*

</td>
<td valign="top">

yes

</td>
<td valign="top">

Identical base type. Here, `*` can be substituted by the empty semantic type. Therefore, `any` is a specialization of `any.*`.

</td>
</tr>
<tr>
<td valign="top">

any

</td>
<td valign="top">

string

</td>
<td valign="top">

yes

</td>
<td valign="top">

Compatible base types and no semantic type.

</td>
</tr>
<tr>
<td valign="top">

stream

</td>
<td valign="top">

any

</td>
<td valign="top">

no

</td>
<td valign="top">

Incompatible base types.

</td>
</tr>
<tr>
<td valign="top">

float64.\*

</td>
<td valign="top">

int64.\*

</td>
<td valign="top">

no

</td>
<td valign="top">

Incompatible base types.

</td>
</tr>
<tr>
<td valign="top">

any.\*

</td>
<td valign="top">

string.\*

</td>
<td valign="top">

yes

</td>
<td valign="top">

Compatible base types and identical semantic type.

</td>
</tr>
<tr>
<td valign="top">

any.\*

</td>
<td valign="top">

string.com.sap

</td>
<td valign="top">

yes

</td>
<td valign="top">

Compatible base types. `com.sap` is a specialization of `*`.

</td>
</tr>
<tr>
<td valign="top">

any.\*

</td>
<td valign="top">

string.com.sap.\*

</td>
<td valign="top">

yes

</td>
<td valign="top">

Compatible base types. `com.sap.*` is a specialization of `*`.

</td>
</tr>
<tr>
<td valign="top">

any.com.sap

</td>
<td valign="top">

any.com.sap

</td>
<td valign="top">

yes

</td>
<td valign="top">

Identical base and semantic types.

</td>
</tr>
<tr>
<td valign="top">

string.com.\*

</td>
<td valign="top">

string.com.sap.\*

</td>
<td valign="top">

yes

</td>
<td valign="top">

Identical base type. `com.*` is a specialization of `com.sap.*`.

</td>
</tr>
<tr>
<td valign="top">

any

</td>
<td valign="top">

any.com

</td>
<td valign="top">

no

</td>
<td valign="top">

Identical base type, but `com` isn't a specialization of the empty semantic type. However, both sides are specializations of `.*`.

</td>
</tr>
<tr>
<td valign="top">

any

</td>
<td valign="top">

any.com.\*

</td>
<td valign="top">

no

</td>
<td valign="top">

Identical base type, but, `com.*` isn't a specialization of the empty semantic type.

</td>
</tr>
</table>

**Related Information**  


[Ports and Port Types](ports-and-port-types-6789999.md "The operator uses ports as an interface to communicate between operators in a graph.")

