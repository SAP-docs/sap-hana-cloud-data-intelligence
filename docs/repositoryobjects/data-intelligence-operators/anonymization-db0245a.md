<!-- loiodb0245aa6d4c4cd0ae746f3b04a98d6a -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Anonymization

Anonymization helps to gain statistically valid insights from your data while protecting the privacy of individuals.



When analyzing data, you must ensure privacy of personal or sensitive information. By removing information that directly identifies an individual, such as a Social Security number or a credit card number, you ensure a certain amount of privacy, but it could still lead to an individual's reidentification.

The Anonymization operator helps to create anonymized groups, where you set the minimum number of records within the group. You have several options for anonymizing data:

-   l-Diversity: Specify the minimum number of distinct sensitive values that must be present in the equivalency class.
-   t-Closeness: Specify how closely the equivalency class distributes values relative to the source table.
-   Mask or generalization: Choose a column to anonymize. For example, if you group individuals into age brackets of 20-29, 30-39, and 40-49, then it’s more difficult to reidentify an individual. When you mask or generalize multiple columns, then the ability to reidentifiy a person or business decreases.

As you use the Anonymization operator, you see the following terms:

-   **Sensitive**: data that most individuals don’t want known about them, for example, salary information or an illness.
-   **Nonsensitive**: data that most individuals may not mind sharing, for example, the country they live in.
-   **Identifier**: data that directly identifies individuals such as their name or Social Security number.
-   **Quasi-identifier**: data that indirectly identifies and individual, especially when combined with other quasi-identifiers, such age, gender, and postcode.

> ### Note:  
> Each business identifies how to categorize the data. What is categorized as nonsensitive for one business may be a quasi-identifier for another business. Any examples shown may be categorized differently based on your needs.



<a name="loiodb0245aa6d4c4cd0ae746f3b04a98d6a__section_gzd_v51_sfb"/>

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

Label

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Enter the name of the data mask operator.

</td>
</tr>
<tr>
<td valign="top">

Minimum rows in anonymized group

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Mandatory. Specifies the minimum rows in a group. Groups with fewer records than the number specified are not output. When the group reaches the specified value, then the group is output. For example, when the operator receives more data, those groups that previously did not have enough records to output may reach the minimum value, and then are output. Any records meeting the criteria of other output groups are immediately added to those groups. Enter a value from 2 to 100. The larger the number you enter, the less likely the data can be reidentified, and a smaller number of records are output. The lower the number entered, the more likely the data can be reidentified and a larger number of records are output.

</td>
</tr>
<tr>
<td valign="top">

End of Data Flag

</td>
<td valign="top">

String

</td>
<td valign="top">

Optional. Specifies the name of the header attribute that indicates whether this input message is the end of the input dataset. When this value is set to `False` in the input message, the data accumulates until the application reads a header attribute value of `True`. After reading the `True` value, the application runs anonymization on all accumulated rows. If you remove the default value and leave the option blank, then anonymization is performed on the first input message, but subsequent input messages generate an error. If you enter an end of data flag that is absent or different from what is in the input message, then anonymization isn’t run.

</td>
</tr>
<tr>
<td valign="top">

Date Format

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Specifies the order in which month, day, and year elements appear in the input string. This value is used only when the day, month, or year in the input string is ambiguous.

</td>
</tr>
<tr>
<td valign="top">

Month Format

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Specifies the format in which the randomized month is output when the software can’t determine the output month format based on the input alone.

For example, the options would output the following for the month of January:

Short: Jan

Full: January

Numeric: 1

</td>
</tr>
<tr>
<td valign="top">

Language

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Specifies the language that the software uses when determining the output of an ambiguous input month string.

</td>
</tr>
<tr>
<td valign="top">

Century Threshold

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Optional. Indicates whether a two-digit date is considered part of the 20th or 21st century. Enter a value from 0 to 99. For example, when set to 25, the dates with a 2-digit value from 00 to 25 result in the years 2000-2025. Dates with a 2-digit value of 26 to 99 result in the years 1926-1999.

</td>
</tr>
<tr>
<td valign="top">

Default Column Behavior

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Define whether to output any columns that are not defined in the *Column Definitions* option.

</td>
</tr>
<tr>
<td valign="top">

Column Definitions

</td>
<td valign="top">

Array

</td>
<td valign="top">

You can define the Anonymization operation on one or more columns. Each column has its own definition. Click :heavy_plus_sign:and complete the following options:

-   Column ID \(string\): Mandatory. This string uniquely identifies the column. It should match the ID or name of the column coming into the operator.
-   Column Designation \(string\): Mandatory. Specifies the categorization and any masking or generalization of this column:
    -   *Sensitive*: Data is output without modification, for example, height. You can choose to make the equivalency groups more secure by setting one or both of these options: *l-Diverstity* and *t-Closeness*.
        -   For *l-Diverstiy*, choose *none* to ignore the *l-Diversity* option. Choose *Distinct l-diversity* to enable this option and to configure the *l-Value*. Set the *l-Value* to a number from 2 through 100. This number specifies the minimum number of distinct sensitive values that must be present in the equivalency class to output the group. For example, if your equivalency class has four distinct values for height \(127 cm, 132 cm, 160 cm, and 193 cm\), and you set the l-Value to 5, then this equivalency class is not output. The equivalency class is output when the option is set to 4.
        -   For *t-Closeness*, choose *none* to ignore the *t-Closeness* option. Choose *Equal distance t-closeness* to enable this option and to configure the *t-Value*. Set the *t-Value* to a number from 0.000001 to 1.0. Entering a number near 0.000001 means that the equivalency class closely distributes the value to the number of times the sensitive value appears in the source table. Entering a value closer to 1.0 means that the distribution is not as reflective to the occurrences in the source table.

    -   *Nonsensitive*: Data is output without modification, for example, hair color.
    -   *Quasi-identifier*: Data is output and used to form equivalence classes, for example, age. You can further mask or generalized the quasi-identifier columns.
        -   *Mask*: Mask all or a portion of the data with another character. For example, a Social Security number might output as \*\*\*-\*\*-1234.
        -   *Date Generalization*: Output date ranges into groups. For example, divide subscribers into groups based on their birth dates, and label the era \(such as Millennials, GenX, Baby Boomers\) rather than using the actual birth date.
        -   *Numeric Generalization*: Output number ranges into groups. For example, output the records in a SALARY column that have values between $42,000 and $125,000 into a group called Middle Class.
        -   *Do Not Modify*: Output data without masking or generalization.

    -   *Identifier*: Data can positively identify an individual and is not output, for example Social Security number.




</td>
</tr>
</table>



<a name="loiodb0245aa6d4c4cd0ae746f3b04a98d6a__section_gjj_fyb_h2b"/>

## Mask Options

Mask all or a portion of the data with another character. For example, a credit card number might output as `****-****-****-1234`.


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

Starting Position

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Specifies whether masking starts at the beginning or end of the value.

</td>
</tr>
<tr>
<td valign="top">

Unmasked Length

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Mandatory. Specifies the number of characters at the beginning or end of the value that should not be masked.

</td>
</tr>
<tr>
<td valign="top">

Masking Character

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. The character or number that replaces the characters in the input data, for example, "\#" or "\*".

</td>
</tr>
<tr>
<td valign="top">

Maintain Formatting

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Mandatory.

-   *True*: retains any special characters such as dashes, slashes, or periods, spaces between characters, and formatting in the output. For example, if you have a phone number that uses dashes, then the dashes are output.
-   *False*: replaces special characters and spaces with the designated masking character.



</td>
</tr>
</table>



<a name="loiodb0245aa6d4c4cd0ae746f3b04a98d6a__section_rs5_qjc_h2b"/>

## Date Generalization Options

Output date ranges into groups.


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

Auto Range Scale

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Defines the scale on which to base the auto range.

-   Not in Use: Indicates that you are not using auto range for the specified input column. This setting is appropriate when you complete the Range Definition options for the input column, or when you don’t use this feature. To define the option, click *\+ Add item*.
-   Calendar Year: Groups records based on the calendar year. The software defines a calendar year as 1/1/yyyy to 12/31/yyyy.
-   Calendar Month: Groups records based on the calendar month. The software defines a calendar month as mm/01/yyyy to mm/eom/yyyy, where "eom" is end of month.



</td>
</tr>
<tr>
<td valign="top">

Minimum Date

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Enter the lowest acceptable date in the range.

> ### Note:  
> Enter a minimum or maximum value, or both. You can’t leave both values empty.



</td>
</tr>
<tr>
<td valign="top">

Minimum Date Inclusive

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Mandatory. Select True when you want to include the minimum date. Select False when you don’t want to include the minimum date in the results. For example, if you set the minimum value to 12/31/2020, then 12/31/2020 is included in the results when True is selected.

</td>
</tr>
<tr>
<td valign="top">

Maximum Date

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Enter the highest acceptable date in the range.

> ### Note:  
> Enter a minimum or maximum value, or both. You can’t leave both values empty.



</td>
</tr>
<tr>
<td valign="top">

Maximum Date Inclusive

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Mandatory. Select True when you want to include the maximum date. Select False when you don’t want to include the maximum date in the results. For example, if you set the maximum date to 06/30/2020, then dates through 06/29/2020 are included in the results when False is selected.

</td>
</tr>
<tr>
<td valign="top">

Replacement Value

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. To describe the group, enter a value.

</td>
</tr>
<tr>
<td valign="top">

Default Replacement Value

</td>
<td valign="top">

String

</td>
<td valign="top">

Optional. Value to output when the input value doesn’t fall into any of the defined ranges.

</td>
</tr>
<tr>
<td valign="top">

Auto Range Duration

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Mandatory. Number of years or months to include in the range.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
<tr>
<td valign="top">

Auto Range Start Date

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Starting date in auto range.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
<tr>
<td valign="top">

Auto Range End Date

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Ending date in auto range.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
<tr>
<td valign="top">

Auto Range Output Format

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Determines the format of the output Auto Range Replacement Value.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
<tr>
<td valign="top">

Auto Range Year Format

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Specifies the number of digits to use for the year. Full Year outputs a four-digit number, for example, 2018. Short Year outputs a two-digit number, for example, 18.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
<tr>
<td valign="top">

Auto Range Month Format

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Determines the month format to use in the Auto Range Replacement Value. Full Text outputs the month name, for example, January. Short Text outputs the abbreviated month name, for example, Jan. Numeric outputs the number of the month, for example, 1 for January.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
<tr>
<td valign="top">

Auto Range Date Delimiter

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Determines the delimiter to use in the Auto Range Replacement Value.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
<tr>
<td valign="top">

Auto Range Numeric Format

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Determines the numeric format to use in the Auto Range Replacement Value.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
<tr>
<td valign="top">

Auto Range Enable Zero Pad

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Optional. Pads a one-digit number with zero when the format includes the month and day. For example, 1/5/2018 changes to 01/05/2018 when set to True.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
<tr>
<td valign="top">

Auto Range Output Language

</td>
<td valign="top">

String

</td>
<td valign="top">

Optional. Determines the language to use in the Auto Range Replacement Value. This setting is applicable when the Month Format is set to Short Text or Full Text.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
</table>



<a name="loiodb0245aa6d4c4cd0ae746f3b04a98d6a__section_xkq_rhc_h2b"/>

## Numeric Generalization Options

Output number ranges into groups. For example, output the records in an `AGE` column that have values between `13-19` into a group called `Teenager`. Specify the ranges to use for numeric variance. In the Numeric Generalization option, select *\+ Add item*.

> ### Note:  
> You can add multiple items.


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

Minimum Value

</td>
<td valign="top">

Decimal

</td>
<td valign="top">

Mandatory. Enter the lowest acceptable value in the range.

> ### Note:  
> Enter a minimum or maximum value, or both. You can’t leave both values empty.



</td>
</tr>
<tr>
<td valign="top">

Minimum Value Inclusive

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Mandatory. Select True when you want to include the minimum value. Select False when you don’t want to include the minimum value in the results. For example, if you set the minimum value to 30, then 30 is included in the results when True is selected.

</td>
</tr>
<tr>
<td valign="top">

Maximum Value

</td>
<td valign="top">

Decimal

</td>
<td valign="top">

Mandatory. Enter the highest acceptable value in the range.

> ### Note:  
> Enter a minimum or maximum value, or both. You can’t leave both values empty.



</td>
</tr>
<tr>
<td valign="top">

Maximum Value Inclusive

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Required. Select True when you want to include the maximum value. Select False when you don’t want to include the maximum value in the results. For example, if you set the maximum value to 50, then numbers through 49 are included in the results when False is selected.

</td>
</tr>
<tr>
<td valign="top">

Replacement Value

</td>
<td valign="top">

String

</td>
<td valign="top">

Optional. To describe the group, enter a value.

</td>
</tr>
<tr>
<td valign="top">

Default Replacement Value

</td>
<td valign="top">

String

</td>
<td valign="top">

Optional. Value to output when the input value doesn’t fall into any of the defined ranges. For example, you might want to label those records as Exceptions.

</td>
</tr>
</table>

**Numeric Generalization Example**

Let's say that you want to assign employees to one of three geographic areas based on their employee number. You would add three items and complete the options as follows.

> ### Sample Code:  
> ```
> Item 0
> Minimum Value: 12000
> Minimum Value Inclusive: True
> Maximum Value: 17000
> Maximum Value Inclusive: False
> Replacement Value: Asia_Pac
> 
> Item 1
> Minimum Value:17000
> Minimum Value Inclusive: True
> Maximum Value: 23000
> Maximum Value Inclusive: False
> Replacement Value: Europe_Africa
> 
> Item 2
> Minimum Value: 23000
> Minimum Value Inclusive: True
> Maximum Value: 28000
> Maximum Value Inclusive: True
> Replacement Value: Americas
> 
> Default Replacement Value: Exceptions
> ```

-   **[Anonymized Groups Example](anonymized-groups-example-2dbdce9.md "Use anonymization to place masked data into match groups so that you can publish data
		without risking reidentification of sensitive data.")**  
Use anonymization to place masked data into match groups so that you can publish data without risking reidentification of sensitive data.

