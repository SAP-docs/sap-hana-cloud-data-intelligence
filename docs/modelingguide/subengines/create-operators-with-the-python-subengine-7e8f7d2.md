<!-- loio7e8f7d22e6d44ca0a78d3e86192d8c8e -->

# Create Operators with the Python Subengine

Create operators in Python using the Python subengine, and use them to build graphs in the SAP Data Intelligence Modeler.



When you run a graph in the Modeler, the main engine that coordinates all subengines breaks the graph into large subgraphs. The advantage is that every operator in the same subgraph is run by the same subengine. The main engine then starts a subengine process for each subgraph.

> ### Note:  
> Python 2.7 is deprecated as of SAP Data Intelligence 1911. Currently, SAP Data Intelligence supports only Python 3.9. You can no longer create new operators based on Python 2.7. Port any existing custom operators based on Python 2.7 to Python 3.9.

> ### Note:  
> When you create a new dockerfile to use in graphs that have Python operators, at minimum you must associate the following tags with the dockerfile: <code>'<b>tornado': '6.1.0</b>'</code>, <code>'<b>sles</b>':</code> '' and <code>'<b>python</b>': '3.9'</code>. Make sure that the resources are installed on the dockerfile.



<a name="loio7e8f7d22e6d44ca0a78d3e86192d8c8e__section_qw4_jd4_cvb"/>

## Data Type Mapping

The following table shows the data type mapping between the Modeler and the Python subengine.


<table>
<tr>
<th valign="top">

Modeler Data Type

</th>
<th valign="top">

Python Subengine Data Type

</th>
</tr>
<tr>
<td valign="top">

string

</td>
<td valign="top">

str

</td>
</tr>
<tr>
<td valign="top">

blob

</td>
<td valign="top">

bytes

</td>
</tr>
<tr>
<td valign="top">

int64

</td>
<td valign="top">

int

</td>
</tr>
<tr>
<td valign="top">

uint64

</td>
<td valign="top">

int

</td>
</tr>
<tr>
<td valign="top">

float64

</td>
<td valign="top">

float

</td>
</tr>
<tr>
<td valign="top">

byte

</td>
<td valign="top">

int

</td>
</tr>
<tr>
<td valign="top">

message

</td>
<td valign="top">

Message

</td>
</tr>
<tr>
<td valign="top">

\[ \]x

Replace the letter `x` with any of the allowed data types, excluding message. For example, \[ \]string, \[ \]uint64, \[ \]blob, and so on.

</td>
<td valign="top">

list

</td>
</tr>
</table>

If you create operators that receive or send data types that have no direct mapping to Modeler data types, you must create ports with type `python 3.9`.

> ### Example:  
> You can connect many Python 3 operators in a graph, all of which have in ports and out ports of type `python 3.9`.

Operators created with ports of type `python 3.9` can communicate with any Python object, including objects with no corresponding Modeler type, such as set, numpy arrays, and so on. There's one exception: Subengine-specific types can't cross the boundary between two Modeler groups. However, if you place your Python-specific object inside the body of a message, then the body is correctly serialized and deserialized with pickle \(a Python module\) when crossing the boundary between two groups.

> ### Note:  
> The behavior of serialization of the body with pickle is specific to the Python subengine; don't expect it to work with other subengines.

Create the message type using the format `Message(body, attributes)`, where:

-   `body` can be any object.
-   `attributes` is a dictionary-mapping string to any object.

If `m` is an object of type message, then you can use the commands `m.body` and `m.attributes` to access the fields initialized in the class constructor. The `attributes` argument is optional in the message constructor. If you want an empty `attributes` string, you can construct your message using the format `Message(body)`.

SAP recommends that you don't use a message inside the body of another message. Instead, use a dictionary inside the body of a message. The dictionary must have the keys "Body" and "Attributes". Using a message object as the body of another message can result in unexpected behavior when you transfer the message across the boundary of different subengines.

> ### Example:  
> The inner message can be converted automatically to a dictionary when crossing the boundaries of different subengines, but it isn't converted back to a message when coming back to your operator's subengine.

Therefore, SAP recommends to always prefer dictionaries over messages inside the body of a message, because it won't change type during the communication.

```
# DO NOT DO THE FOLLOWING:
inner_msg = Message("body_of_inner_msg")
outer_msg = Message(body=inner_msg, attributes={})
```

```
# If you want to have a message as the body of another message, do this instead:
inner_msg = {"body": "body_of_inner_msg"}
outer_msg = Message(inner_msg)
```



<a name="loio7e8f7d22e6d44ca0a78d3e86192d8c8e__section_tbf_sf4_cvb"/>

## Methods to Create Python Operators

Use one of the following two methods to create your own Python operators:

-   **Normal usage:** To create normal Python subengines, use only the Modeler user interface.
-   **Advanced usage:** To create new Python operators, use the advanced method, which shows you how to use your own machine and then upload the new operators to SAP Data Intelligence. The advanced usage method of creating operators is useful when you want to code in your own IDE and create unit tests for your operators.

-   **[Normal Usage](normal-usage-0daa121.md "If you want to create simple scripts quickly, we recommend that you customize the
		behavior of operators using the SAP Data Intelligence
		Modeler user interface.")**  
If you want to create simple scripts quickly, we recommend that you customize the behavior of operators using the SAP Data Intelligence Modeler user interface.
-   **[Advanced Usage](advanced-usage-1ef5a1e.md "You can create operators without using the Modeler user interface. ")**  
You can create operators without using the Modeler user interface.

