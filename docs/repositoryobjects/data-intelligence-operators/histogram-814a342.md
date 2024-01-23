<!-- loio814a342d58604c93b3af32de1716ffe2 -->

# Histogram

The Histogram operator receives a numeric value as input and increments the counter of the bin that corresponds to the range in which the value lies. The array of counts is then sent in the output port.



<a name="loio814a342d58604c93b3af32de1716ffe2__section_sq1_nf3_vdb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Parameter

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

Number of Bins

</td>
<td valign="top">

nBins

</td>
<td valign="top">

int

</td>
<td valign="top">

The number of bins of the histogram. It must be greater than zero.

Default: 10

</td>
</tr>
<tr>
<td valign="top">

Range Min

</td>
<td valign="top">

rangeMin

</td>
<td valign="top">

float64

</td>
<td valign="top">

The minimum value on the x axis. Input values lower than `Range Min` are ignored.

Default: 0.0

</td>
</tr>
<tr>
<td valign="top">

Range Max

</td>
<td valign="top">

rangeMax

</td>
<td valign="top">

float64

</td>
<td valign="top">

The maximum value on the x axis. Input values higher than `Range Max` are ignored.

Default: 1.0

</td>
</tr>
<tr>
<td valign="top">

Output on nth Input

</td>
<td valign="top">

outputEveryNInput

</td>
<td valign="top">

uint64

</td>
<td valign="top">

Sends an accumulated histogram on every `Output on nth Input` values received in the input port. It is sent only if the histogram has changed since the last send \(it may not have changed if the values received were out of range\).

Default: 1

</td>
</tr>
<tr>
<td valign="top">

Output Period \(s\)

</td>
<td valign="top">

outputPeriodInSec

</td>
<td valign="top">

float64

</td>
<td valign="top">

Sends an accumulated histogram every `Output Period (s)` seconds. It is sent only if the histogram has changed since the last send \(it may not have changed if the values received were out of range\).

Default: 0.0

</td>
</tr>
</table>

> ### Note:  
> Either *Output on nth input* or *Output Period \(s\)* must be set \(greater to zero\), but not both.



<a name="loio814a342d58604c93b3af32de1716ffe2__section_knq_5f3_vdb"/>

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

`histIn` 

</td>
<td valign="top">

any.\*

</td>
<td valign="top">

A numeric value that is converted to float64. It can be a string or blob that represents a numeric value or a golang primitive numeric type.

</td>
</tr>
</table>



<a name="loio814a342d58604c93b3af32de1716ffe2__section_swc_cg3_vdb"/>

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

`histOut` 

</td>
<td valign="top">

message

</td>
<td valign="top">

A Data Pipeline message with the histogram in the body as an array of uint64, and the message header has the `Range Min` and `Range Max` from the configuration.

</td>
</tr>
</table>

