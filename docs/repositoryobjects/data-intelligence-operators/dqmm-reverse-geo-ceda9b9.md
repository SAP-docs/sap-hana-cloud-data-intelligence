<!-- loioceda9b91eac440938c6f4d6ab92e6e28 -->

# DQMm Reverse Geo

With the DQMm Reverse Geo operator, you can prepare reverse geocoding requests to be sent to the SAP Data Quality Management, microservices for location data.



SAP Data Quality Management, microservices for location data offers cloud-based microservices for address cleansing, geocoding, and reverse geocoding. You can embed address cleansing and enrichment services within any business process or application so that you can quickly reap the value of complete and accurate address data.

This operator will create requests from your data that can then be passed to the DQMm Client operator.



<a name="loioceda9b91eac440938c6f4d6ab92e6e28__section_sq1_nf3_vdb"/>

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

outputFields

</td>
<td valign="top">

string

</td>
<td valign="top">

The list of result field names separated by commas that specify the fields from the service that will be output.

Default: default: "geo\_search\_results, geo\_search\_results\_count, geo\_info\_code, geo\_info\_code\_msg"

The original input fields will be included in the output. If an output field name has the same name as an input field, then the input field will be overwritten on output. If you wish to retain the original input, you should map the output field to a different name.

</td>
</tr>
<tr>
<td valign="top">

radius

</td>
<td valign="top">

numberA

</td>
<td valign="top">

One way to reduce the number of addresses returned is by including a maximum distance, which represents the radius of a circle with center at the geo-location coordinates sent in the request. All returned addresses are within the limits of this circle. The value for radius must be a positive number. If a radius is between 0 and 1, prefix the number with a zero \(for example, 0.4\).

Default: 1.0

</td>
</tr>
<tr>
<td valign="top">

distanceUnit

</td>
<td valign="top">

string

</td>
<td valign="top">

Either kilometers or miles.

Default: "kilometers"

For example, to obtain a list of addresses within 10 km from the geo-location coordinates, set:

```
radius = 10.0
  distanceUnit = kilometers
```

To obtain a list of addresses within a half mile, set:

```
radius = 0.5
  distanceUnit = miles
```

When omitted from the request, the default distance is 1 kilometer. The maximum distance supported by the service is 111 kilometers or 68.97 miles, which represents one degree of latitude. If the request is sent with a distance greater than the maximum, then the service's maximum value is used.

</td>
</tr>
<tr>
<td valign="top">

maxRecords

</td>
<td valign="top">

number

</td>
<td valign="top">

A second way to reduce the number of addresses returned is by including a maximum number of records. The value for maxRecords may be between 1 and 100, sent as a data type of integer. When omitted from the request, the default maximum number of records is 100.

Default: 100

</td>
</tr>
<tr>
<td valign="top">

passThroughField

</td>
<td valign="top">

string

</td>
<td valign="top">

The field within the data to be returned unchanged in the response.

</td>
</tr>
</table>



<a name="loioceda9b91eac440938c6f4d6ab92e6e28__section_knq_5f3_vdb"/>

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

`input` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The input expected to be in JSON format.

</td>
</tr>
</table>



<a name="loioceda9b91eac440938c6f4d6ab92e6e28__section_swc_cg3_vdb"/>

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

`output` 

</td>
<td valign="top">

message

</td>
<td valign="top">

The output is in JSON format.

</td>
</tr>
</table>

