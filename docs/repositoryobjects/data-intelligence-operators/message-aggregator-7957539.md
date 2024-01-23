<!-- loio79575394ef4c45c7886aef7ec30247c2 -->

# Message Aggregator

The Message Aggregator operator aggregates input messages in a custom manner specified by JavaScript functions that the user can enter.



<a name="loio79575394ef4c45c7886aef7ec30247c2__section_sq1_nf3_vdb"/>

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

Script

</td>
<td valign="top">

script

</td>
<td valign="top">

script

</td>
<td valign="top">

Contains either the script to be executed or the path to the script. For a script, the string must start with "file://".

Default: "file://default.js"

</td>
</tr>
<tr>
<td valign="top">

Partial Aggregation

</td>
<td valign="top">

partialAggregation

</td>
<td valign="top">

bool

</td>
<td valign="top">

Specify true for partial aggregation. Specify false for global aggregation.

Default: false

</td>
</tr>
<tr>
<td valign="top">

Convert Input Body to Type

</td>
<td valign="top">

convertInputBodyToType

</td>
<td valign="top">

string

</td>
<td valign="top">

Specify a type name for the input message body to be converted into before being passed as an argument to the JavaScript function. Accepted type names: `blob` \(for an array of bytes\), `string`, `bool` and all primitive numeric types from golang. Maps and arrays of types other than byte are currently not supported. Be aware that not all conversions are possible and the [Golang conversion](https://golang.org/ref/spec#Conversions) rules apply.

</td>
</tr>
<tr>
<td valign="top">

Convert Output Body to Type

</td>
<td valign="top">

convertOutputBodyToType

</td>
<td valign="top">

string

</td>
<td valign="top">

Similar to convertInBodyToType, but it converts the output message body right after the JavaScript function is returned and before the message is sent to the output channel. In addition to the same supported type names from convertInBodyToType, the string "input" is also supported, and uses the input to the JavaScript function for the conversion of its output.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Ignore Group Key

</td>
<td valign="top">

ignoreGroupKey

</td>
<td valign="top">

any

</td>
<td valign="top">

If the key returned by the getGroupKey\(msg\) function is equal to the ignoreGroupKey, then the message received is not passed to the aggregate function.

Default: false

</td>
</tr>
</table>



<a name="loio79575394ef4c45c7886aef7ec30247c2__section_knq_5f3_vdb"/>

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

message

</td>
<td valign="top">

The input message to be aggregated.

</td>
</tr>
</table>



<a name="loio79575394ef4c45c7886aef7ec30247c2__section_swc_cg3_vdb"/>

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

message

</td>
<td valign="top">

The aggregated message result.

</td>
</tr>
</table>



<a name="loio79575394ef4c45c7886aef7ec30247c2__section_lkm_w2m_fhb"/>

## Basic Example 1: Summing with Global Aggregation

When the `Partial Aggregation` parameter is set to false, then the operator expects the user to specify three JavaScript functions:

-   getGroupKey: Specifies in which group the received message is aggregated.

-   canRelease: Determines if a given group can already be aggregated and emitted to the out channel.

-   aggregate: Performs the actual aggregation logic upon a group list of messages.


For example:

```
function getGroupKey(msg) {
	return msg.Body%2;
}
function canRelease(list) {
	return list.length >= 5;
}
function aggregate(list) {
	var sum = 0;
	for (var i = 0; i < list.length; i++) {
		sum += list[i].Body;
	}
	var msg = {};
	msg.Body = sum;
	msg.Attributes = {};
	return msg;
}
```



<a name="loio79575394ef4c45c7886aef7ec30247c2__section_mf5_r4c_12b"/>

## Basic Example 2: Summing with Partial Aggregation

When the `Partial Aggregation` option is set to true, then the operator expects the user to specify three JavaScript functions:

-   getGroupKey: Specifies in which group the received message is aggregated.

-   partialAggregate: Performs a partial aggregation and holds its state inside the JavaScript environment. The key is also passed in case the user wants to use it for grouping. The partialAggregate function also should return a bool indicating if the aggregate for the key should be released.

-   getAggregation: Returns the aggregation for the key passed as argument.


For example:

```
var msgGroupState = {};
function getGroupKey(msg) {
	return msg.Body%2;
}
function partialAggregate(key, m) {
	var doRelease = false;
	if (!(key in msgGroupState)) {
		msgGroupState[key] = [m.Body, 1];
		return doRelease;
	}
	var state = msgGroupState[key];
	state[0] += m.Body ;
	state[1] += 1;
	if (state[1] === 5) {
		doRelease = true;
	}
	msgGroupState[key] = state;
	return doRelease;
}
function getAggregation(key) {
	var aggr = msgGroupState[key][0];
	delete msgGroupState[key];
	var msg = {};
	msg.Body = aggr;
	msg.Attributes = {"key": key};
	return msg;
}

```

