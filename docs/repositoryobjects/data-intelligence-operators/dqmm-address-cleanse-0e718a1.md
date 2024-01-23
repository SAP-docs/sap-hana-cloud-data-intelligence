<!-- loio0e718a1ee46e4f7aae86431623d61072 -->

# DQMm Address Cleanse

With the DQMm Address Cleanse operator, you can prepare address cleanse requests to be sent to the SAP Data Quality Management, microservices for location data.



SAP Data Quality Management, microservices for location data offers cloud-based microservices for address cleansing, geocoding, and reverse geocoding. You can embed address cleansing and enrichment services within any business process or application so that you can quickly reap the value of complete and accurate address data.

This operator will create requests from your data that can then be passed to the DQMm Client operator.



<a name="loio0e718a1ee46e4f7aae86431623d61072__section_sq1_nf3_vdb"/>

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

configurationName

</td>
<td valign="top">

string

</td>
<td valign="top">

The name of the configuration to use if configSource is specified as DQM Microservices.

</td>
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

Default: "std\_addr\_address\_delivery, std\_addr\_locality, std\_addr\_region, std\_addr\_postcode\_full, std\_addr\_country\_2char"

The original input fields will be included in the output. If an output field name has the same name as an input field, then the input field will be overwritten on output. If you wish to retain the original input, you should map the output field to a different name.

</td>
</tr>
<tr>
<td valign="top">

processingMode

</td>
<td valign="top">

string

</td>
<td valign="top">

-   empty: Default value. Use the default service value or the value present in the configuration if one is specified.

-   both: The service cleanses address data and appends geo-location coordinates, provided the request includes output fields from both processes.
-   addressOnly: The service performs only cleansing address data, not appending geo-location coordinates. If the request includes output fields for the geo-location process, the values for those fields will be empty in the response. In this mode, a transaction is counted for the address, but not for the geo-location.
-   geoOnly: The service performs only appending geo-location coordinates, not cleansing address data. If the request includes output fields for the cleansed address, the values for those fields will be empty in the response. In this mode, a transaction is counted for the geo-location, but not for the address. This mode should be used only when the address data sent in the request has previously gone through address cleansing, or when you have high confidence in the quality of the address data.

Default: "both"

</td>
</tr>
<tr>
<td valign="top">

casing

</td>
<td valign="top">

string

</td>
<td valign="top">

-   \(empty\) : Default value. Use the default service value or the value present in the configuration if one is specified.

-   mixed : Use mixed case. Example: 100 Main St

-   upper : Use all uppercase. Example: 100 MAIN ST


Default: "mixed"

</td>
</tr>
<tr>
<td valign="top">

diactrics

</td>
<td valign="top">

string

</td>
<td valign="top">

-   \(empty\) : Default value. Use the default service value or the value present in the configuration if one is specified.

-   include: Include diacritical characters. Example: Münchner Str 100

-   remove: Remove diacritical characters. Example: Muenchner Str 100


Default: "include"

</td>
</tr>
<tr>
<td valign="top">

streetFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

-   \(empty\): Default value. Use the default service value or the value present in the configuration if one is specified.

-   countryCommonStyle: Abbreviate or use the full form of street address components based on what is most common for each country. See countryCommonStyle.

-   abbreviateNoPunctuation: Abbreviate street type, street prefix or suffix, and secondary designator. No punctuation is inserted. Example: 100 N Main St Ste 300

-   abbreviateWithPunctuation: Abbreviate street type, street prefix or suffix, and secondary designator. Punctuation is inserted for each abbreviated word. Example: 100 N. Main St. Ste. 300

-   expand: Use the full form of street type, street prefix or suffix, and secondary designator. Example: 100 North Main Street Suite 300

-   expandPrimaryAbbreviateSecondaryNoPunctuation: Use the full form of street type and street prefix or suffix; abbreviate secondary designator. No punctuation is inserted. Example: 100 North Main Street Ste 300

-   expandPrimaryAbbreviateSecondaryWithPunctuation : Use the full form of street type and street prefix or suffix; abbreviate secondary designator. Punctuation is inserted for each abbreviated word. Example: 100 North Main Street Ste. 300

Default: "countryCommonStyle"

</td>
</tr>
<tr>
<td valign="top">

postalFormal

</td>
<td valign="top">

string

</td>
<td valign="top">

-   \(empty\): Default value. Use the default service value or the value present in the configuration if one is specified.

-   countryCommonStyle: Abbreviate or use the full form of the postbox designator based on what is most common for each country. See countryCommonStyle.

-   abbreviateNoPunctuation: Abbreviate the postbox designator. No punctuation is inserted. Example: PO Box 100

-   abbreviateWithPunctuation: Abbreviate the postbox designator. Punctuation is inserted for each abbreviated word. Example: P.O. Box 100

-   expand: Use the full form of the postbox designator. Example: Post Office Box 100


Default: "countryCommonStyle"

</td>
</tr>
<tr>
<td valign="top">

regionFormat

</td>
<td valign="top">

string

</td>
<td valign="top">

-   \(empty\): Default value. Use the default service value or the value present in the configuration if one is specified.

-   countryCommonStyle: Abbreviate or use the full form of the region based on what is most common for each country. See countryCommonStyle.

-   abbreviate: Abbreviate the region. Example: CA

-   expand: Use the full region name. Example: California


Default: "countryCommonStyle"

</td>
</tr>
<tr>
<td valign="top">

scriptConversion

</td>
<td valign="top">

string

</td>
<td valign="top">

-   \(empty\): Default value. Use the default service value or the value present in the configuration if one is specified.

-   none: Preserve the script. Do not convert.

-   convertToLatin: Convert the script to Latin. Supported only for the following countries and regions:

    -   China
    -   Taiwan
    -   Republic of Korea
    -   Russian Federation


Default: "preserve"

</td>
</tr>
<tr>
<td valign="top">

minAssignmentLevel

</td>
<td valign="top">

string

</td>
<td valign="top">

-   \(empty\): Default value. Use the default service value or the value present in the configuration if one is specified.

-   none: The service charges for the transaction and returns cleansed address results provided the address meets the billable transaction criteria, regardless of the address assignment level.

-   city: The service charges for the transaction and returns cleansed address results when the address assignment level is city \(L1\) or better. When the address assignment level is lower than city, the service does not charge for the transaction, and it returns address results that are formatted but not corrected.

-   street: The service charges for the transaction and returns cleansed address results when the address assignment level is street \(PN\) or better. When the address assignment level is lower than street, the service does not charge for the transaction, and it returns address results that are formatted but not corrected.

-   houseNumber: The service charges for the transaction and returns cleansed address results when the address assignment level is house number \(PR\) or better. When the address assignment level is lower than house number, the service does not charge for the transaction, and it returns address results that are formatted but not corrected.


Default: "none"

</td>
</tr>
<tr>
<td valign="top">

geoAssign

</td>
<td valign="top">

string

</td>
<td valign="top">

-   \(empty\): Default value. Use the default service value or the value present in the configuration if one is specified.

-   best: Returns geo-location coordinates that represent points of the actual address. When this fine level of assignment is not possible, then return points that represent the centroid point of the geometric shape represented by part or the entire postcode. When that is not possible, then return points that represent the centroid point of the geometric shape represented by the city.

-   houseNumberOnly: Returns geo-location coordinates that represent points of the actual address. For each address that this fine level of assignment is not possible, then do not return geo-location coordinates at all.


Default: "best"

</td>
</tr>
<tr>
<td valign="top">

suggestionSuppressLevel

</td>
<td valign="top">

string

</td>
<td valign="top">

-   \(empty\): Default value. Use the default service value or the value present in the configuration if one is specified.

-   none: The service returns suggestions when there is ambiguity at any level when matching the input address with reference data.

-   secondary: The service returns suggestions when there is ambiguity when matching the input postcode, city, region, or primary portion of the street address with reference data. However, the suggestions feature is suppressed when there is ambiguity when matching the secondary portion of the street address, such as apartment, suite, unit, or floor.


Default: "none"

</td>
</tr>
<tr>
<td valign="top">

generateSuggestionList

</td>
<td valign="top">

string

</td>
<td valign="top">

Indicates whether it is possible for the microservice to generated suggestion lists.

Default: "no"

</td>
</tr>
<tr>
<td valign="top">

suggestionReplyField

</td>
<td valign="top">

string

</td>
<td valign="top">

The field within the data to be used as a suggestion reply when performing address cleansing with suggestion lists enabled.

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



<a name="loio0e718a1ee46e4f7aae86431623d61072__section_knq_5f3_vdb"/>

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



<a name="loio0e718a1ee46e4f7aae86431623d61072__section_swc_cg3_vdb"/>

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

