<!-- loio6330e231dbb94ecd8588a682e0f00410 -->

# Wiretap V2

The Wiretap operator can wiretap a connection between two operators in a Pipeline Engine graph and display the traffic to the browser window or to an external WebSocket client that connects to this operator.



To view the traffic, open the UI window using the context menu of this operator after the graph has started. If the operator is started in a group with multiplicity, the traffic from one instance is displayed.

The tapping can be statically disabled at the starting of the graph or can be toggled later if the graph is started with the tapping enabled.

The Wiretap operator does not buffer any data. It streams the incoming Message to the next operator and therefore requires the stream to be consumed. A graph that is idle and stuck in running state may indicate that the Wiretap is waiting for the next operator to read from the input body.



<a name="loio6330e231dbb94ecd8588a682e0f00410__section_jgr_wwf_zdb"/>

## Configuring the Output Format

One can customize the layout parameter to display the traffic data in some specific format or to hide some parts of data, such as unimportant or sensitive data. The default format produces a line with the date and the message.

The following table lists the layout format specifiers and their usage:

**Layout format specifiers and their usage**


<table>
<tr>
<th valign="top">

Specifier

</th>
<th valign="top">

Description

</th>
<th valign="top">

Usage Samples

</th>
</tr>
<tr>
<td valign="top">

%i

</td>
<td valign="top">

The index number of the entry.

</td>
<td valign="top">

%i

</td>
</tr>
<tr>
<td valign="top">

%d

</td>
<td valign="top">

The customizable formatted date.

</td>
<td valign="top">

%d, %d\{yyyy-MM-ddTHH:mm:ss.SSS\}

</td>
</tr>
<tr>
<td valign="top">

%g

</td>
<td valign="top">

The group node name.

</td>
<td valign="top">

%g

</td>
</tr>
<tr>
<td valign="top">

%m

</td>
<td valign="top">

The entire message or payload.

</td>
<td valign="top">

%m

</td>
</tr>
<tr>
<td valign="top">

%r

</td>
<td valign="top">

The time in milliseconds since the wiretap has started.

</td>
<td valign="top">

%r

</td>
</tr>
<tr>
<td valign="top">

%n

</td>
<td valign="top">

The newline.

</td>
<td valign="top">

%n

</td>
</tr>
</table>

The following table shows some sample parameter samples.

**Sample parameter samples**


<table>
<tr>
<th valign="top">

Sample Layout

</th>
<th valign="top">

Sample Output

</th>
</tr>
<tr>
<td valign="top">

\(%g\)\[%d\]%m

</td>
<td valign="top">

\(graph-1\)\[2019-03-04 16:51:10,000\]\{"ID": "\\u0000\\u0000..", "body": "hello world","headers":\[\{"ID":"metadata","filename":"hello.txt","chars":10\}\]\}

</td>
</tr>
<tr>
<td valign="top">

%m

</td>
<td valign="top">

\{"ID": "\\u0000\\u0000..", "body": "hello world","headers":\[\{"ID":"metadata","filename":"hello.txt","chars":10\}\]\}

</td>
</tr>
<tr>
<td valign="top">

%r - \[%m\]

</td>
<td valign="top">

1522 - \{"ID": "\\u0000\\u0000..", "body": "hello world","headers":\[\{"ID":"metadata","filename":"hello.txt","chars":10\}\]\}

</td>
</tr>
</table>



<a name="loio6330e231dbb94ecd8588a682e0f00410__section_vsk_ns2_qqb"/>

## UI Page

The UI page shows some menu and status information at the top and the tapped traffic data underneath.

The connection status at the right upper corner indicates the number of instances running and connected to.

The *Tapping* button enables the tapping to be turned on or off during the operation.

Finally, the *Layout* and *Max Size* buttons allow the layout pattern and the max size property to be modified during the operation.

> ### Note:  
> The tapping consumes processing resources, especially when the data is complex, as the data needs to be serialized into a printable format.

These buttons on the UI page can be used to interactively adjust the behavior of the Wiretap operator during its operation.


<table>
<tr>
<th valign="top">

UI Menu

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Clear Output

</td>
<td valign="top">

Clear the output panel.

</td>
</tr>
<tr>
<td valign="top">

Tapping On/Off

</td>
<td valign="top">

Toggle the tapping mode.

</td>
</tr>
<tr>
<td valign="top">

Layout

</td>
<td valign="top">

Show or change the `layout` parameter.

</td>
</tr>
<tr>
<td valign="top">

Max Size

</td>
<td valign="top">

Show or change the `maxSize` parameter.

</td>
</tr>
<tr>
<td valign="top">

String Length

</td>
<td valign="top">

Show or change the `truncateStringLength` parameter.

</td>
</tr>
<tr>
<td valign="top">

Table Rows

</td>
<td valign="top">

Show or change the `truncateTableRows` parameter.

</td>
</tr>
<tr>
<td valign="top">

Type Information

</td>
<td valign="top">

Show or change the `printTypeInformation` parameter.

</td>
</tr>
<tr>
<td valign="top">

Headers

</td>
<td valign="top">

Show or change the `printHeaders` parameter.

</td>
</tr>
<tr>
<td valign="top">

Body

</td>
<td valign="top">

Show or change the `printBody` parameter.

</td>
</tr>
<tr>
<td valign="top">

Pretty Print

</td>
<td valign="top">

Show or change the `prettyPrint` parameter.

</td>
</tr>
</table>



<a name="loio6330e231dbb94ecd8588a682e0f00410__section_sq1_nf3_vdb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Disabled

</td>
<td valign="top">

disable

</td>
<td valign="top">

bool

</td>
<td valign="top">

Disables the output when this parameter is set to *true*.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Max. Size

</td>
<td valign="top">

maxSize

</td>
<td valign="top">

int

</td>
<td valign="top">

The maximal size of the message to be displayed in the wiretap. Any message larger than this size will be truncated when displayed.

Default: 4092

</td>
</tr>
<tr>
<td valign="top">

Spool Size

</td>
<td valign="top">

spoolSize

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of preceding messages that are spooled at the operator and can be sent to the display that has started or reconnected. This spool size is truncated by its maximal size of 256. When the operator is disabled or the tapping is turned off, messages are not spooled.

Default: 32

</td>
</tr>
<tr>
<td valign="top">

Layout

</td>
<td valign="top">

layout

</td>
<td valign="top">

string

</td>
<td valign="top">

The layout pattern to format each line using the conversion characters. The layout pattern can be changed from the UI page.

Default: "\[%d\] %m"

</td>
</tr>
<tr>
<td valign="top">

Truncate String Length

</td>
<td valign="top">

truncateStringLength

</td>
<td valign="top">

integer

</td>
<td valign="top">

The maximum number of characters displayed for any single attribute. "0" can be used for an unlimited amount of characters.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Truncate Table Rows

</td>
<td valign="top">

truncateTableRows

</td>
<td valign="top">

integer

</td>
<td valign="top">

The maximum number of rows printed per table \(if the incoming message is a table\). "0" can be used for an unlimited amount of rows.

Default: 0

</td>
</tr>
<tr>
<td valign="top">

Print Type Information

</td>
<td valign="top">

printTypeInformation

</td>
<td valign="top">

bool

</td>
<td valign="top">

Specifies if detailed type information should be displayed or not.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Print Headers

</td>
<td valign="top">

printHeaders

</td>
<td valign="top">

bool

</td>
<td valign="top">

Specifies if the message headers should be displayed or not.

Default: true

</td>
</tr>
<tr>
<td valign="top">

Print Body

</td>
<td valign="top">

printBody

</td>
<td valign="top">

bool

</td>
<td valign="top">

Specifies if the message body should be displayed or not.

Default: true

</td>
</tr>
<tr>
<td valign="top">

Pretty Print

</td>
<td valign="top">

prettyPrint

</td>
<td valign="top">

bool

</td>
<td valign="top">

Specifies if the output should be pretty printed or not.

Default: true

</td>
</tr>
</table>



<a name="loio6330e231dbb94ecd8588a682e0f00410__section_knq_5f3_vdb"/>

## Input


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Type

</th>
<th valign="top">

Type ID

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`in` 

</td>
<td valign="top">

\*

</td>
<td valign="top">

\*

</td>
<td valign="top">

Input to this wiretap.

</td>
</tr>
</table>



<a name="loio6330e231dbb94ecd8588a682e0f00410__section_swc_cg3_vdb"/>

## Output


<table>
<tr>
<th valign="top">

Output

</th>
<th valign="top">

Type

</th>
<th valign="top">

Type ID

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`out` 

</td>
<td valign="top">

\*

</td>
<td valign="top">

\*

</td>
<td valign="top">

Output from this wiretap. This port may be left unconnected.

</td>
</tr>
</table>

