<!-- loio6c73a5fcb7a249ab83876c2350357fe5 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Data Mask

Protect the personally identifiable or sensitive information by covering all or a portion of the data.



Some examples of personal and sensitive data include credit card numbers, birth dates, tax identification numbers, salary information, medical identification numbers, bank account numbers, and so on. Use data masking to support security and privacy policies, and to protect your customer or employee data from possible theft or exploitation.

Place the Data Mask operator toward the end of your graph to ensure that all columns that are to be masked have undergone processing by upstream operators. If you place Data Mask before other operators, the downstream operators may not process the actual data but rather the masked data. In some cases, the operator isn't able to process the columns at all if Data Mask replaced input data with blanks or a masking character such as “\#”.



<a name="loio6c73a5fcb7a249ab83876c2350357fe5__section_tbl_mwb_h2b"/>

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

Seed

</td>
<td valign="top">

String

</td>
<td valign="top">

Optional. An alpha or numeric string. Set this option to mask the data in a way that ensures consistent output values each time the data is output. One seed value maintains referential integrity for the following variance types set up in the Data Mask transform: Number Variance, Date Variance, and Pattern Variance.

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

Required. Specifies the order in which month, day, and year elements appear in the input string. This value is used only when the day, month, or year in the input string is ambiguous.

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

Required. Specifies the format in which the randomized month is output when the software cannot determine the output month format based on the input alone.

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

Required. Specifies the language that the software uses when determining the output of an ambiguous input month string.

</td>
</tr>
<tr>
<td valign="top">

Century Threshold

</td>
<td valign="top">

String

</td>
<td valign="top">

Optional. Indicates whether a two-digit date is considered part of the 20th or 21st century. Enter a value from 0-99. For example, when set to 25, the dates with a 2-digit value from 00-25 result in the years 2000-2025. Dates with a 2-digit value of 26-99 result in the years 1926-1999.

</td>
</tr>
<tr>
<td valign="top">

Column Definitions

</td>
<td valign="top">

 

</td>
<td valign="top">

You can define the mask operation on one or more columns. Each column has its own definition. Click :heavy_plus_sign:and complete the following options:

-   Column ID \(string\): Required. This string uniquely identifies the column. It should match the ID or name of the column coming into the operator.
-   Operation \(string\): Required. Specifies the type of masking operation for this column: Mask, Pattern Variance, Numeric Variance, Numeric Generalization, Date Variance, or Date Generalization.



</td>
</tr>
</table>



<a name="loio6c73a5fcb7a249ab83876c2350357fe5__section_gjj_fyb_h2b"/>

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

Required. Specifies whether masking starts at the beginning or end of the value.

</td>
</tr>
<tr>
<td valign="top">

Unmasked Length

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. Specifies the number of characters at the beginning or end of the value that are not masked.

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

Required. The character or number that replaces the characters in the input data, for example, "\#" or "\*".

</td>
</tr>
<tr>
<td valign="top">

Maintain Formatting

</td>
<td valign="top">

String

</td>
<td valign="top">

Required.

-   True: retains any special characters such as dashes, slashes or periods, spaces between characters, and formatting in the output. For example, if you have a phone number that uses dashes, then the dashes are output.
-   False: replaces special characters and spaces with the designated masking character.



</td>
</tr>
</table>



<a name="loio6c73a5fcb7a249ab83876c2350357fe5__section_j2f_wyb_h2b"/>

## Pattern Variance Options

Mask an input substring with a specific pattern. For example, using the part number `ABC123GHI`, mask the first three characters with `ZYW`, mask the next three characters with `999`, and preserve the final three characters as input. The result would be `ZYW999GHI`. In the Pattern Variance Definition option, select *\+ Add item*.

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

Variance Type

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. Choose one of the options.

-   Default: Masks each applicable character with the like characters for alpha and numeric content. Retains spaces and special characters.
-   Preserve: Outputs the defined substring the same as it is input.
-   Character: Masks the defined substring by randomly placing each of the characters in the defined substring with the values that you specify in the Value setting. Retains spaces and special characters.
-   String: Masks the defined substring by randomly replacing the entire substring with values that you specify in the Value option. Does not retain spaces or special characters.



</td>
</tr>
<tr>
<td valign="top">

Starting Position

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Required. A positive integer that indicates the character number where masking starts. Alpha, numeric, space, and other printable characters are included in the position count.

</td>
</tr>
<tr>
<td valign="top">

Length

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Required. A positive integer that indicates the number of positions \(characters\) to mask.

</td>
</tr>
<tr>
<td valign="top">

Value

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. When parsing the string for a value, it trims leading and trailing spaces from the value. You can maintain the spaces by surrounding the value in framing characters such as double quotes. For example, STRING, "John,Smith". If the value has double quotes, you can escape the double quotes using a backslash. For example, "\\"Slim\\"". If the value with framing characters has a backslash in it, the backslash can be escaped with an additional backslash. For example, "\\\\path".

> ### Note:  
> The Value option is visible only when Variance Type is set to Character or String.



</td>
</tr>
</table>



<a name="loio6c73a5fcb7a249ab83876c2350357fe5__section_rgp_xg5_mlb"/>

## Pattern Variance Regular Expression

Mask an input substring with a regular expression. Use a regular expression to break a piece of data into groups, and then mask each group using a different variance type. For example, you could have email addresses with variable lengths like `jon.gi1l@ai.com` and `stephanie.milkowski@business.com`. You can create a regular expression breaking the value into 4 groups: username, @ symbol, domain, and domain extension. Define each group and assign a variance type to each group.


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

Regular Expression

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. Enter a regular expression. If you have defined multiple groups using the parenthesis \(\), define each group by clicking the link next to Pattern Variance Regex Definition.

</td>
</tr>
<tr>
<td valign="top">

Pattern Variance Regex Definition

</td>
<td valign="top">

Array

</td>
<td valign="top">

Define how you want each regular expression group to be masked. Click :heavy_plus_sign: to create groups.

> ### Note:  
> You can create multiple groups.



</td>
</tr>
<tr>
<td valign="top">

Group Number

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. Enter the number of a group that was defined in the reqular expression option.

</td>
</tr>
<tr>
<td valign="top">

Variance Type

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. Choose one of the options.

-   Default: Masks each applicable character with the like characters for alpha and numeric content. Retains spaces and special characters.
-   Preserve: Outputs the defined substring the same as it is input.
-   Character: Masks the defined substring by randomly placing each of the characters in the defined substring with the values that you specify in the Value setting. Retains spaces and special characters.
-   String: Masks the defined substring by randomly replacing the entire substring with values that you specify in the Value option. Does not retain spaces or special characters.



</td>
</tr>
<tr>
<td valign="top">

Value

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. When parsing the string for a value, it trims leading and trailing spaces from the value. You can maintain the spaces by surrounding the value in framing characters such as double quotes. For example, STRING, "John,Smith". If the value has double quotes, you can escape the double quotes using a backslash. For example, "\\"Slim\\"". If the value with framing characters has a backslash in it, the backslash can be escaped with an additional backslash. For example, "\\\\path".

> ### Note:  
> The Value option is visible only when Variance Type is set to Character or String.



</td>
</tr>
</table>



<a name="loio6c73a5fcb7a249ab83876c2350357fe5__section_jbv_sgc_h2b"/>

## Numeric Variance Options

Output randomized numbers. For example, change the input salary of 50,000 to a random number between 45,000-55,000.


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

Numeric Variance Type

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. Define how you want to vary a number.

-   Percentage: Varies the data by a percentage that is within a calculated minimum and maximum range.
-   Fixed Number: Varies the data by a fixed number that is within a calculated minimum and maximum range.
-   Range: Varies the data that is greater than or equal to the user-defined minimum value and less than or equal to the user-defined maximum values that you set. You must set the minimum and maximum values.



</td>
</tr>
<tr>
<td valign="top">

Numeric Variance

</td>
<td valign="top">

Number

</td>
<td valign="top">

Required. Determines the number by which to randomize the input. Enter a value greater than zero.

</td>
</tr>
<tr>
<td valign="top">

Minimum Value

</td>
<td valign="top">

Number

</td>
<td valign="top">

Required. Determines the number by which to randomize the input. Enter the lowest value that can be output as a whole number or decimal. Negative decimal numbers are supported. For best results, set a realistic maximum value.

> ### Note:  
> The Minimum Value is required only when the Numeric Variance Type is set to Range.



</td>
</tr>
<tr>
<td valign="top">

Maximum Value

</td>
<td valign="top">

Number

</td>
<td valign="top">

Required. Enter the highest value that can be output as a whole number or decimal. Negative numbers are supported. For best results, set a realistic maximum value.

> ### Note:  
> The Minimum Value is required only when the Numeric Variance Type is set to Range.



</td>
</tr>
</table>



<a name="loio6c73a5fcb7a249ab83876c2350357fe5__section_xkq_rhc_h2b"/>

## Numeric Generalization Options

Output numbers ranges into groups. For example, output the records in an `AGE` column that have values from `13 to 19` into a group called `Teenager`. Specify the ranges to use for numeric variance. In the Numeric Generalization option, select *\+ Add item*.

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

Integer

</td>
<td valign="top">

Enter the lowest acceptable value in the range.

> ### Note:  
> Enter a minimum or maximum value, or both. You cannot leave both values empty.



</td>
</tr>
<tr>
<td valign="top">

Minimum Value Inclusive

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. Select True when you want to include the minimum value. Select False when you do not want to include the minimum value in the results. For example, if you set the minimum value to 30, then 30 is included in the results when True is selected.

</td>
</tr>
<tr>
<td valign="top">

Maximum Value

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Enter the highest acceptable value in the range.

> ### Note:  
> Enter a minimum or maximum value, or both. You cannot leave both values empty.



</td>
</tr>
<tr>
<td valign="top">

Maximum Value Inclusive

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. Select True when you want to include the maximum value. Select False when you do not want to include the minimum value in the results. For example, if you set the maximum value to 50, then numbers through 49 are included in the results when False is selected.

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

Optional. Enter a value to describe the group.

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

Optional. Value to output when the input value does not fall into any of the defined ranges. For example, you could label those records as Exceptions.

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



<a name="loio6c73a5fcb7a249ab83876c2350357fe5__section_nl1_djc_h2b"/>

## Date Variance Options

Output randomized dates. For example, change the input date of 01/15/2017 to a random date between 01/01/2017 and 01/31/2017.


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

Date Variance Type

</td>
<td valign="top">

String

</td>
<td valign="top">

Specifies how you want to vary a date.

-   Range: Varies the date within the user-defined minimum and maximum dates that you set. You must set the Minimum and Maximum date values.
-   Fixed Days: Varies the date by a fixed number of days that occur before or after the input date.
-   Fixed Months: Varies the date by a fixed number of months that occur before or after the input month.
-   Fixed Years: Varies the date by a fixed number of years that occur before or after the input year.



</td>
</tr>
<tr>
<td valign="top">

Date Variance

</td>
<td valign="top">

Number

</td>
<td valign="top">

Required. Determines the number of days, months, or years by which to randomize the input. The value must be greater than zero.

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

Required for Range; optional for other types. Specify the minimum date allowed on output.

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

Required for Range; optional for other types. Specify the maximum date allowed on output.

</td>
</tr>
</table>



<a name="loio6c73a5fcb7a249ab83876c2350357fe5__section_rs5_qjc_h2b"/>

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

Required. Defines the scale on which to base the auto range.

-   Not in Use: Indicates that you are not using auto range for the specified input column. This setting is appropriate when you complete the Range Definition options for the input column, or when you do not use this feature. Click *\+ Add item* to further define the option.
-   Calendar Year: Group records based on the calendar year. The software defines a calendar year as 1/1/yyyy to 12/31/yyyy.
-   Calendar Month: Group records based on the calendar month. The software defines a calendar month as mm/01/yyyy to mm/eom/yyyy, where "eom" is end of month.



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

Enter the lowest acceptable date in the range.

> ### Note:  
> Enter a minimum or maximum value, or both. You cannot leave both values empty.



</td>
</tr>
<tr>
<td valign="top">

Minimum Date Inclusive

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. Select True when you want to include the minimum date. Select False when you do not want to include the minimum date in the results. For example, if you set the minimum value to 12/31/2020, then 12/31/2020 is included in the results when True is selected.

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

Enter the highest acceptable date in the range.

> ### Note:  
> Enter a minimum or maximum value, or both. You cannot leave both values empty.



</td>
</tr>
<tr>
<td valign="top">

Maximum Date Inclusive

</td>
<td valign="top">

String

</td>
<td valign="top">

Required. Select True when you want to include the maximum date. Select False when you do not want to include the minimum date in the results. For example, if you set the maximum date to 06/30/2020, then dates through 06/29/2020 are included in the results when False is selected.

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

Required. Enter a value to describe the group.

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

Optional. Value to output when the input value does not fall into any of the defined ranges.

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

Required. Number of years or months to include in the range.

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

Required. Starting date in auto range.

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

Required. Ending date in auto range.

> ### Note:  
> This option is only visible Auto Range Scale is set to Calendar Month or Calendar Year.



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

Required. Determines the format of the output Auto Range Replacement Value.

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

Required. Specifies the number of digits to use for the year. Full Year outputs a four-digit number, for example, 2018. Short Year outputs a two-digit number, for example, 18.

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

Required. Determines the month format to use in the Auto Range Replacement Value. Full Text outputs the month name, for example, January. Short Text outputs the abbreviated month name, for example, Jan. Numeric outputs the number of the month, for example, 1 for January.

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

Required. Determines the delimiter to use in the Auto Range Replacement Value.

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

Optional. Determines the numeric format to use in the Auto Range Replacement Value.

> ### Note:  
> This option is visible only when Auto Range Scale is set to Calendar Month or Calendar Year.



</td>
</tr>
<tr>
<td valign="top">

Auto Range Enable Zero Pad

</td>
<td valign="top">

String

</td>
<td valign="top">

Optional. Pad a one-digit number with zero when the format includes the month and day. For example, 1/5/2018 changes to 01/05/2018 when set to True.

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



<a name="loio6c73a5fcb7a249ab83876c2350357fe5__section_dqr_q4c_h2b"/>

## Input

> ### Note:  
> Only string and number are valid data types for input columns.


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

Input

</td>
<td valign="top">

Message

</td>
<td valign="top">

The input is expected to be in JSON format.

</td>
</tr>
</table>



<a name="loio6c73a5fcb7a249ab83876c2350357fe5__section_ozn_x4c_h2b"/>

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

Output

</td>
<td valign="top">

BLOB

</td>
<td valign="top">

The output is in JSON format.

</td>
</tr>
</table>

-   **[Data Mask Examples](data-mask-examples-77192ae.md "Examples of Mask, Date Generalization, Date Variance, Numeric Generalization, Numeric
		Variance, and Pattern Variance masking options show how various settings affect the
		data.")**  
Examples of Mask, Date Generalization, Date Variance, Numeric Generalization, Numeric Variance, and Pattern Variance masking options show how various settings affect the data.

