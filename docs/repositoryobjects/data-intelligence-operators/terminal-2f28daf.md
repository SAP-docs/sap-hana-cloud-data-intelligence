<!-- loio2f28daff1a8348b7a069cb92d4225442 -->

# Terminal

The Terminal operator represents a terminal window in the browser.



It consists of an output area on top and an input area. The output area is bound to the input port `in1`. The input area is bound to the output port `out1`.

The areas can be resized by dragging the frame separator.



<a name="loio2f28daff1a8348b7a069cb92d4225442__section_pcr_r3r_1fb"/>

## Display Areas

-   *Output*: Displays in real time the data received from another operator through the bound port `in1`. May add a prefix or a suffix to each message as set in `Layout`. Received multi-line strings will count as only one message and display on multiple lines, receiving only one layout formatting. The number of lines to be kept on screen is limited by the *Line Limit* field, and its default value is `500` \(setting it to `0` removes the limit\). When opening the terminal or reconnecting after a period of disconnection, an automatic discontinuity message may be shown, indicating how many messages were lost in the time it was not connected. If all the messages were still present in the back end spool, they will all be sent and no discontinuity message will be shown. The discontinuity marker is not available when `Spool Size` is set to `0`.

    When dealing with large amounts of data, it is important to mind the number of lines \(*Line Limit*\) and Bytes/line \(`maxSize`\) limits, in order to avoid crashing the front-end terminal.

-   *Input*: Allows sending edited data to other operators through the bound port `out1`. Will send literal strings as they appear on screen when [Enter\] is pressed. To add a newline feed, use [Shift-Enter\]. A list of all available shortcuts can be accessed at the *Keyboard Shortcuts* button.



<a name="loio2f28daff1a8348b7a069cb92d4225442__section_kzj_v3r_1fb"/>

## Menu Options

-   *Clear Input/Clear Output*: Clears the content of the corresponding area.
-   *Line Limit*: Limits the number of lines that will be shown at the *Output* area. Press [Enter\] after inserting the number to refresh. Setting this to `0` will remove line limit and display as many lines as the machine can receive or process.

    Default: 500

-   *Keyboard Shortcuts*: Displays a pop-on dialog with the Input and shortcuts for editing commands.



<a name="loio2f28daff1a8348b7a069cb92d4225442__section_sq1_nf3_vdb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

ID

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

Setting this to *true* disables the output processing in the back end.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Max Size \(bytes\)

</td>
<td valign="top">

maxSize

</td>
<td valign="top">

int

</td>
<td valign="top">

The maximum size of each message in Bytes to be displayed in the Terminal. Any message larger than the given size will be truncated when displayed.

Default: 1024

</td>
</tr>
<tr>
<td valign="top">

Spool Size \(messages\)

</td>
<td valign="top">

spoolSize

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of preceding messages that are spooled and sent to the display that has started at some later time. Has a hard limit of 10000 messages.

Default: 100

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

The layout pattern to display each inputted message, consisting of literal characters and the following pieces:

-   `%m`: The received string message.

-   `%d`: Timestamp.

-   `%n`: Newline feed.

-   `%r`: Time \(milliseconds\) between operator creation and message reception at back end component.


Default: "\[%d\] %m%n"

</td>
</tr>
</table>



<a name="loio2f28daff1a8348b7a069cb92d4225442__section_knq_5f3_vdb"/>

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

Description

</th>
</tr>
<tr>
<td valign="top">

`in1` 

</td>
<td valign="top">

string.\*

</td>
<td valign="top">

Input string to be displayed on terminal output area.

</td>
</tr>
</table>



<a name="loio2f28daff1a8348b7a069cb92d4225442__section_swc_cg3_vdb"/>

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

Description

</th>
</tr>
<tr>
<td valign="top">

`out1` 

</td>
<td valign="top">

string.\*

</td>
<td valign="top">

Output string from terminal input area.

</td>
</tr>
</table>

