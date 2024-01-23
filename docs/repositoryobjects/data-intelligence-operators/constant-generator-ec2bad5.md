<!-- loioec2bad5f397542288af38666068ec1e2 -->

# Constant Generator

The Constant Generator operator represents a constant string that may be emitted into the graph. It can do so on a regular basis \('pulse' mode\) or only once \('once' mode\). The 'in' port can be used only to start the string constant operator when an incoming signal is received.



<a name="loioec2bad5f397542288af38666068ec1e2__section_sq1_nf3_vdb"/>

## Configuration Parameters


<table>
<tr>
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

content

</td>
<td valign="top">

string

</td>
<td valign="top">

The content that the string constant emits.

</td>
</tr>
<tr>
<td valign="top">

mode

</td>
<td valign="top">

string

</td>
<td valign="top">

There are three modes: once, pulse and trigger:

-   once: In this mode, the content is emitted only once.

-   pulse: In this mode, the content is emitted repeatedly by the specified duration.

-   trigger: In this mode, the content is emitted every time a signal is received by the in-port.




</td>
</tr>
<tr>
<td valign="top">

duration

</td>
<td valign="top">

string

</td>
<td valign="top">

If in pulse mode, the duration between ticks where the content is emitted.

</td>
</tr>
<tr>
<td valign="top">

counter

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of times this component has to receive any incoming signal to start running.

</td>
</tr>
</table>



<a name="loioec2bad5f397542288af38666068ec1e2__section_knq_5f3_vdb"/>

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

`in` 

</td>
<td valign="top">

any

</td>
<td valign="top">

Incoming signals that reduce the 'counter' and trigger output in 'trigger' mode.

</td>
</tr>
</table>



<a name="loioec2bad5f397542288af38666068ec1e2__section_swc_cg3_vdb"/>

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

`out` 

</td>
<td valign="top">

string

</td>
<td valign="top">

The content.

</td>
</tr>
</table>

