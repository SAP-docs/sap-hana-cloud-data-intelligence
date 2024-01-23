<!-- loio77192ae0bd084452ade93830b4736680 -->

# Data Mask Examples

Examples of Mask, Date Generalization, Date Variance, Numeric Generalization, Numeric Variance, and Pattern Variance masking options show how various settings affect the data.



<a name="loio77192ae0bd084452ade93830b4736680__section_mjl_55p_j2b"/>

## Mask

Masking a portion of data:

-   If you have a column for User\_ID, the value is `Smith7887`, and you set the option to *Everything except the first 4 characters*, your output would be `Smitxxxxx`.
-   If you set the same option to *Everything except the last 2 characters*, your output would be `xxxxxxx87`. If your masking character is left blank, your output would be `87`.

Using the *Maintain format* option:

-   If you have a column for Phone1, the value is `800-555-1234`, and then select *Maintain format*, your output would be `xxx-xxx-xxxx`. Not selecting this option would output `xxxxxxxxxxxx`.
-   If you have a column for Email1, the value is `john.smith@abc.com`, and you enable *Maintain format* and *Mask all characters in email name*, then your output would be `xxxxxxxxxx@xxx.xxx`.
-   If you enable *Maintain format* and disable *Mask all characters in email name*, then your output would be `xxxx.xxxxx@xxx.xxx`.
-   If you disable both *Maintain format* and *Mask all characters in email name*, then your output would be `xxxxxxxxxxxxxxxxxx`.



<a name="loio77192ae0bd084452ade93830b4736680__section_cvz_bwp_j2b"/>

## Date Generalization

Let's say that you want to divide subscribers into groups based on their birth dates, and that you want to label the era rather than using the actual birth date. Because the age groups are not an equal number of years, it would be best to manually define each range one at a time rather than using the auto range. The default masked value is defined as `Out of Range`, so that any records that do not belong in the defined ranges will output `Out of Range` as the masked value.


<table>
<tr>
<th valign="top">

Minimum

</th>
<th valign="top">

Column Name

</th>
<th valign="top">

Maximum

</th>
<th valign="top">

Masked Value

</th>
</tr>
<tr>
<td valign="top">

1940.01.01<=

</td>
<td valign="top">

BIRTHDATE

</td>
<td valign="top">

<=1964.12.31

</td>
<td valign="top">

Baby Boomer

</td>
</tr>
<tr>
<td valign="top">

1965.01.01<=

</td>
<td valign="top">

BIRTHDATE

</td>
<td valign="top">

<=1976.12.31

</td>
<td valign="top">

Gen X

</td>
</tr>
<tr>
<td valign="top">

1977.01.01<=

</td>
<td valign="top">

BIRTHDATE

</td>
<td valign="top">

<=1995.12.31

</td>
<td valign="top">

Millennial

</td>
</tr>
</table>



<a name="loio77192ae0bd084452ade93830b4736680__section_vfw_swp_j2b"/>

## Date Variance

The following table shows several examples for one date value in a database: `May 27, 1995`. The examples help to illustrate how the date is calculated internally, and how it is output when the user-defined minimum and maximum values are used together.


<table>
<tr>
<th valign="top">

Variance Type

</th>
<th valign="top">

Internally calculated date

</th>
<th valign="top">

Output value within this range

</th>
<th valign="top">

Notes

</th>
</tr>
<tr>
<td valign="top">

Fixed Days

Variance: 10

Minimum date: <not set\>

Maximum date: <not set\>

</td>
<td valign="top">

Min date: May 17, 1995

Max date: Jun 6, 1995

</td>
<td valign="top">

Min date: May 17, 1995

Max date: Jun 6, 1995

</td>
<td valign="top">

Max date: Jun 6, 1995

</td>
</tr>
<tr>
<td valign="top">

Fixed Days

Variance: 100

Minimum date: Mar 1, 1995

Maximum date: Aug 31, 1995

</td>
<td valign="top">

Min date: Feb 9, 1995

Max date: Sep 4, 1995

</td>
<td valign="top">

Min date: Mar 1, 1995

Max date: Aug 31, 1995

</td>
<td valign="top">

The user-defined minimum and maximum dates are within the calculated minimum and maximum dates. Therefore, the user-defined dates are used.

</td>
</tr>
<tr>
<td valign="top">

Fixed Months

Variance: 6

Min date: Jan 1, 1995

Max date: Dec 31, 1995

</td>
<td valign="top">

Min date: Nov 27, 1994

Max date: Nov 27, 1995

</td>
<td valign="top">

Min date: Jan 1, 1995

Max date: Nov 27, 1995

</td>
<td valign="top">

The user-defined minimum date is within the calculated variance, and is the value used for output.

The maximum user-defined date is outside of the calculated variance. Therefore, the maximum calculated date is used.

</td>
</tr>
<tr>
<td valign="top">

Fixed Years

Variance: 15

Min date: Jan 1, 1965

Max date: Dec 31, 2015

</td>
<td valign="top">

Min date: May 27, 1980

Max date: May 27, 2010

</td>
<td valign="top">

Min date: May 27, 1980

Max date: May 27, 2010

</td>
<td valign="top">

Both of the user-defined minimum and maximum dates are outside of the calculated variance. Therefore the calculated date is used.

</td>
</tr>
<tr>
<td valign="top">

Range

Min date: Jan 1, 1965

Max date: Dec 31, 2015

</td>
<td valign="top">

n/a

</td>
<td valign="top">

Min date: Jan 1, 1965

Max date: Dec 31, 2015

</td>
<td valign="top">

Because there is no variance for range, only the user-defined minimum and maximum values are used.

</td>
</tr>
</table>



<a name="loio77192ae0bd084452ade93830b4736680__section_z1j_h1q_j2b"/>

## Numeric Generalization

Let's say that you want to categorize your employee numbers by location. Rather than outputting the employee number, the defined masked values replace the value in the EMPNO column. Any numbers that do not fall into the range have the default masked value, `Outliers`.


<table>
<tr>
<th valign="top">

Minimum

</th>
<th valign="top">

Column Name

</th>
<th valign="top">

Maximum

</th>
<th valign="top">

Masked Value

</th>
</tr>
<tr>
<td valign="top">

12000<=

</td>
<td valign="top">

EMPNO

</td>
<td valign="top">

<=16999

</td>
<td valign="top">

Asia\_Pac

</td>
</tr>
<tr>
<td valign="top">

17000<=

</td>
<td valign="top">

EMPNO

</td>
<td valign="top">

<=29999

</td>
<td valign="top">

Europe\_Africa

</td>
</tr>
<tr>
<td valign="top">

23000<

</td>
<td valign="top">

EMPNO

</td>
<td valign="top">

<=28999

</td>
<td valign="top">

Americas

</td>
</tr>
</table>



<a name="loio77192ae0bd084452ade93830b4736680__section_fkj_s1q_j2b"/>

## Numeric Variance

The following table shows several examples for one salary value in a database: `$50,000`. The examples help to illustrate how the value is calculated internally, and how it is output when the user-defined minimum and maximum values are used together.


<table>
<tr>
<th valign="top">

Variance Type

</th>
<th valign="top">

Internally calculated value

</th>
<th valign="top">

Output within this range

</th>
<th valign="top">

Notes

</th>
</tr>
<tr>
<td valign="top">

Percentage

Variance: 25

Minimum value: <not set\>

Maximum value: <not set\>

</td>
<td valign="top">

Min value: $37,500

Max value: $62,500

</td>
<td valign="top">

Min value: $37,500

Max value: $62,500

</td>
<td valign="top">

The output uses the internally calculated values, because the user-defined values are not specified.

</td>
</tr>
<tr>
<td valign="top">

Percentage

Variance: 25

Minimum value: 45,000

Maximum value: 85,000

</td>
<td valign="top">

Min value: $37,500

Max value: $62,500

</td>
<td valign="top">

Min value: $45, 00

Max value: $62,500

</td>
<td valign="top">

The user-defined minimum value is within the calculated variance, and is the value used for output.

The maximum user-defined date is outside of the calculated variance. Therefore, the maximum calculated value is used.

</td>
</tr>
<tr>
<td valign="top">

Fixed number

Variance: 2500

Minimum value: <not set\>

Maximum value: <not set\>

</td>
<td valign="top">

Min value: $47,500

Max value: $52,500

</td>
<td valign="top">

Max value: $52,500

Max value: $52,500

</td>
<td valign="top">

The output uses the internally calculated values, because the user-defined values are not specified.

</td>
</tr>
<tr>
<td valign="top">

Fixed number

Variance: 2500

Minimum value: 45,000

Maximum value: 85,000

</td>
<td valign="top">

Min value: $47,500

Max value: $52,500

</td>
<td valign="top">

Min value: $47,500

Max value: $52,500

</td>
<td valign="top">

Both the user-defined minimum and maximum values are outside of the calculated variance. Therefore, the calculated minimum and maximum values are used.

</td>
</tr>
<tr>
<td valign="top">

Range

Minimum value: 55,000

Maximum value: 95,000

</td>
<td valign="top">

n/a

</td>
<td valign="top">

Minimum value: 55,000

Maximum value: 95,000

</td>
<td valign="top">

Because there is no variance for range, only the user-defined minimum and maximum values are used.

</td>
</tr>
</table>



<a name="loio77192ae0bd084452ade93830b4736680__section_n1f_z2q_j2b"/>

## Pattern Variance

-   **Default variance type:** The following table describes how the default pattern variance masks input characters with like characters.


    <table>
    <tr>
    <th valign="top">

    Input character type
    
    </th>
    <th valign="top">

    Mask values
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Alphabetic
    
    </td>
    <td valign="top">
    
    Masks lowercase alpha character with random lowercase alpha character.

    Masks uppercase alpha character with random uppercase alpha character.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Numeric
    
    </td>
    <td valign="top">
    
    Masks each numeric character with a random numeric character from 0 up to and including 9.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Special characters or spaces
    
    </td>
    <td valign="top">
    
    Does not mask special characters or spaces, but outputs them as they are input, unmasked. For example, when the input substring contains a dash \(-\), the default pattern variance keeps the dash in the output. When the input substring contains a space, the default pattern variance keeps the space in the output.
    
    </td>
    </tr>
    </table>
    
    The following table shows the best practice use of default pattern variance.


    <table>
    <tr>
    <th valign="top">

    Description
    
    </th>
    <th valign="top">

    Best Practice
    
    </th>
    <th valign="top">

    Example
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Mask an entire input field using the default pattern variance.
    
    </td>
    <td valign="top">
    
    Add a substring definition with a Default variance type.
    
    </td>
    <td valign="top">
    
    Starting position: 1

    Ending position: <slider all the way to the right\>
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Automatically apply the default pattern variance to substrings of a mapped input column that are not defined.
    
    </td>
    <td valign="top">
    
    Define input field substrings using one or more of the other pattern variance types, and leave portions of the input value undefined.
    
    </td>
    <td valign="top">
    
    **Definition 1:**

    Definition type: Preserve

    Starting position: 1

    Ending position: 3

    **Definition 2:**

    Definition type: String

    Starting position: 4

    Ending position: 5

    Value range min-max: 20-25

    Undefined range: 6 through the end of the value

    **Results**

    Definition 1: Preserves the characters in positions 1-3

    Definition 2: Masks the entire substring \(position 4-5\) with a number that is included in the minimum and maximum range \(in this case 20-25\)

    Undefined: Masks position six through the end of the field with the default pattern variance.
    
    </td>
    </tr>
    </table>
    
-   **Preserve variance type:** The application outputs the defined substring as it was input, with no masking.

    > ### Note:  
    > The default pattern variance is applied to any undefined portions of the input column. Undefined portions are the sections of the input column that have not been defined with preserve, character, or string pattern variance.

    The following table contains an example of the preserve pattern variance.


    <table>
    <tr>
    <th valign="top">

    Strategy
    
    </th>
    <th valign="top">

    Settings
    
    </th>
    <th valign="top">

    Example input and output
    
    </th>
    <th valign="top">

    Notes
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Preserve the unit identification number in each record. Mask the rest of the value with the default pattern variance.
    
    </td>
    <td valign="top">
    
    **Undefined:** Character in position 1

    **Definition:**

    Definition type: Preserve

    Starting position: 2

    Ending position: 3

    Value: <blank\>

    **Undefined:** Characters 4 through the end of the value
    
    </td>
    <td valign="top">
    
    Input value: `B12:G350`

    Possible output values, preserved characters in bold.

    <code>A<b>12</b>:N799</code>

    <code>F<b>12</b>:M127</code>
    
    </td>
    <td valign="top">
    
    **Undefined:** Masks the first position with a like character using the default pattern variance.

    **Definition:** Preserves position two and three with the preserve pattern variance \(in this case the numbers 12\).

    **Undefined:** masks the fourth position to the end of the string using the default pattern variance.

    The colon in the input field \(character four\) is included in the undefined portion. The software outputs the colon as it was input based on the default pattern variance definition.
    
    </td>
    </tr>
    </table>
    
-   **Character variance type:** The application masks each character in the defined substring with a character from the Value option.

    The Value option can include individual uppercase or lowercase alpha characters, numeric characters from 0 to 9, ranges of alpha characters, or ranges of numeric characters \(using numbers from 0 to 9\), spaces, special characters \(such as @, \#, \_, &\), or any combination of these.

    > ### Note:  
    > Each alpha and numeric value must be one character in length. Also, you can use only one character for minimum and maximum values when using a value range.

    Special characters are output as they are input, without masking them, when they are present in a defined substring for character pattern variance.

    The following table contains an example of the character pattern variance.


    <table>
    <tr>
    <th valign="top">

    Strategy
    
    </th>
    <th valign="top">

    Settings
    
    </th>
    <th valign="top">

    Example input and output
    
    </th>
    <th valign="top">

    Notes
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Mask an identification code with specific alpha or numeric values, and apply the default pattern variance to the remaining portion of the value.
    
    </td>
    <td valign="top">
    
    **Undefined:** character in position 1

    **Definition:**

    Definition type: Character

    Starting position: 2

    Ending position: 3

    Value: `J-L|B|W-Y|2`

    Undefined: characters 4 through the end of the value
    
    </td>
    <td valign="top">
    
    Input value: `123a`

    Possible output values, masked characters in bold.

    <code>8<b>KB</b>x</code>

    <code>3<b>2W</b>t</code>
    
    </td>
    <td valign="top">
    
    **Undefined:** Masks the first position with a like character using the default pattern variance.

    **Definition:** Masks position two and three using the character pattern variance and randomly chooses a character specified in the *Value* field to mask each position.

    **Undefined:** Masks the fourth position to the end of the string using the default pattern variance.
    
    </td>
    </tr>
    </table>
    
-   **String variance type:**The application masks the entire defined substring with a random character or string from the *Value* option.

    The *Value* option can include one or more alpha or numeric characters \(such as `MILK` or `2458`\), spaces, special characters \(such as @, \#, \_, &\), numeric ranges, or any combination of these in a list in the *Value* option.

    The application counts all alphanumeric characters, spaces, and special characters when it determines the substring length. However, the application does not retain the special characters or spaces in the output when they are present in a defined substring for string pattern variance.

    The following table contains an example of the string pattern variance.


    <table>
    <tr>
    <th valign="top">

    Strategy
    
    </th>
    <th valign="top">

    Settings
    
    </th>
    <th valign="top">

    Example input and output
    
    </th>
    <th valign="top">

    Notes
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Preserve the product code, but mask the type of milk \(white, chocolate, soy, and so on\) with the general term `MILK`.
    
    </td>
    <td valign="top">
    
    **Definition 1:**

    Definition type: Preserve

    Starting position: 1

    Ending position: 5

    Value: <blank\>

    **Definition 2:**

    Definition type: String

    Starting position: 6

    Ending position: <end of column\>

    Value: `MILK`
    
    </td>
    <td valign="top">
    
    Input value: `5428-WTMLK`

    `5429-SOYMLK`

    Possible output values, string characters in bold.

    <code>5428-<b>MILK</b></code>

    <code>5429-<b>MILK</b></code>
    
    </td>
    <td valign="top">
    
    **Definition 1:** Preserves the first through the fifth positions, including the dash, as part of preserve pattern variance. The dash is output as it was input because it is included in the preserve pattern variance.

    **Definition 2:** Masks position six to the end of the field with the value `MILK`.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Include a zero to the left of any number in a range \(to the left of the lower or higher number or to both numbers\) so the mask value is left-padded with zeros for the length of the substring.

    > ### Note:  
    > Zero-padding numbers in a range are applicable for string pattern variance only.


    
    </td>
    <td valign="top">
    
    **Definition 1:**

    Definition type: String

    Starting position: 1

    Ending position: 5

    Value: `01-8|999`

    **Undefined:** position 6 through the end of the column.
    
    </td>
    <td valign="top">
    
    Input value: `04-a1099`

    Possible output values, string characters in bold.

    <code><b>00003</b>502</code>

    <code><b>999</b>832</code>
    
    </td>
    <td valign="top">
    
    **Definition 1:** Outputs the first through the fifth characters with a number from 1 up to and including 8, or the number 999.

    When the application chooses a number from the range as a mask value, it zero-pads the number to the left so the masked value is the length of the defined substring \(5 characters\).

    The application does not zero-pad the number 999 because it does not contain a leading zero in the Value option.

    The application includes the dash in the input field in the position count for the substring. However, the application does not output the dash as part of the string pattern variance definition.

    **Undefined:** The application applies the default pattern variance to the undefined portion of the input field, character six to the end of the field, and replaces each numeric value with a random value from 0 to 9.
    
    </td>
    </tr>
    </table>
    
-   Examples of various pattern variance types by showing example definition option settings, input values, and possible output values.


    <table>
    <tr>
    <th valign="top">

    Strategy
    
    </th>
    <th valign="top">

    Settings
    
    </th>
    <th valign="top">

    Example Input and Output
    
    </th>
    <th valign="top">

    Notes
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Mask the weight and the unit of measure from a product code, but preserve the product type.
    
    </td>
    <td valign="top">
    
    **Definition 1:**

    Definition type: Preserve

    Starting position: 1

    Ending position: 3

    Value: <blank\>

    **Undefined:** Position 4 and 5.

    **Definition 2:**

    Definition type: String

    Starting position: 6

    Ending position: 9

    Value: `GAL|qt|pt|oz|CUP`
    
    </td>
    <td valign="top">
    
    Input value: `MLK12CUP`

    Possible output values:

    `MLK63GAL`

    `MLK18pt`

    `MLK04oz`
    
    </td>
    <td valign="top">
    
    **Definition 1:** Preserves the first three positions using the preserve pattern variance.

    **Undefined:** Masks the fourth and fifth positions using the default pattern variance, which replaces each numeric character with a value from 0-9.

    **Definition 2:** Masks the sixth through the eighth positions with one of the values listed using the string pattern variance.

    In some cases, the software replaces a 3-character substring with a 2-character value.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Mask the product type and the weight from a product code, but preserve the unit of measure.
    
    </td>
    <td valign="top">
    
    **Definition 1:**

    Definition type: String

    Starting position: 1

    Ending position: 3

    Value: `ALMLK| SOYMLK| RCEMLK| WTMLK| CHMLK`

    **Definition 2:**

    Definition type: String

    Starting position: 4

    Ending position: 5

    Value:`01-12| 32| 16`

    **Definition 3:**

    Definition type: Preserve

    Starting position: 6

    Ending position: <end of column\>

    Value: <blank\>
    
    </td>
    <td valign="top">
    
    Input value: `MLK12CUP`

    Possible output values:

    `WTMLK32CUP`

    `RCEMLK16CUP`

    `ALMLK08CUP`
    
    </td>
    <td valign="top">
    
    **Definition 1:** Masks the first three positions using one of the values specified for string pattern variance.

    The application masks the 3-character substring with values that may be longer than 3 characters.

    **Definition 2:** Masks the fourth and fifth positions using the string pattern variance.

    The first value listed in the Value option for Definition 2 is a range beginning with a zero-padded number. This ensures that the mask value is the length of the defined substring, 2 characters.

    **Definition 3:** Preserves the sixth through the eighth positions.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Mask the number of paper sheets per package, and the type of packaging from the product description column.
    
    </td>
    <td valign="top">
    
    **Definition 1:**

    Definition type: Character

    Starting position: 1

    Ending position: 4

    Value: 0-9

    **Undefined:**Position 5.

    **Definition 2:**

    Definition type: String

    Starting position: 6

    Ending position: <end of column\>

    Value: `Ream| Case| Pack| Box`
    
    </td>
    <td valign="top">
    
    Input value: `1500/Ream`

    Possible output values:

    `0950/Case`

    `8945/Box`

    `2639/Pack`
    
    </td>
    <td valign="top">
    
    **Definition 1:** Masks the first through the fourth positions with a number from 0 to 9.

    The user could leave the first through the fifth position undefined so the application masks the substring using the default pattern variance to get similar output values. The forward slash would be output as part of the substring in this case.

    **Undefined:** Outputs the forward slash \(/\) character in the fifth position using the default pattern variance \(maintains special characters on output\).

    **Definition 2:** Masks the sixth position to the end of the column with one of the character strings listed in the Value option.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Mask the school district, the state, and the enrollment number. Preserve the type of school.
    
    </td>
    <td valign="top">
    
    **Definition 1:**

    Definition type: String

    Starting position: 1

    Ending position: 3

    Value: `DST`

    **Definition 2:**

    Definition type: String

    Starting position: 4

    Ending position: 5

    Value: `ST`

    Undefined: Position 6, 7, 8, and 9.

    **Definition 3:**

    Definition type: Preserve

    Starting position: 10

    Ending position: <end of column\>

    Value: <blank\>
    
    </td>
    <td valign="top">
    
    Input value: `INDNE7321MID`

    `ANMA7321HIGH`

    `SNBCA7321ELEM`

    Possible output values:

    `DSTST3829MID`

    `DSTST5784HIGH`

    `DSTST0789ELEM`

    > ### Note:  
    > The mask out variance could also mask the fields in this example. However, with pattern variance, you can distinguish between parts of the whole string and have more control over the mask values.


    
    </td>
    <td valign="top">
    
    **Definition 1:** Masks position one to three with the string `DST`.

    **Definition 2:** Masks the fourth and the fifth position with the string `ST`.

    **Undefined:** Masks position six through nine with the default pattern variance.

    **Definition 3:** Preserves the tenth position to the end of the column.
    
    </td>
    </tr>
    </table>
    



<a name="loio77192ae0bd084452ade93830b4736680__section_ozf_21b_nlb"/>

## Pattern Variance Regular Expression

Using a regular expresion is useful when the data values are not a specific length. You can use regular expressions on any type of data. In this example, we'll use email addresses. Let's say that you have these email addresses: `jon.gill@ai.com` and `stephanie.milkowski@business.com`. You can create a regular expression breaking the value into 4 parts: username, @ symbol, domain, and domain extension. Define each group and assign a variance type to each group. Here is an example of the regular expression that you can use: `^([^@]*)(@)([^.]*)(.*)$`. First, let's break down the regular expression.


<table>
<tr>
<th valign="top">

Part of Regular Expression

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`^`

</td>
<td valign="top">

The first caret `^` identifies the beginning of the string.

</td>
</tr>
<tr>
<td valign="top">

`([^@]*)`

</td>
<td valign="top">

This is the first group of the expression identified by the parentheses `()`. The brackets, caret and `@` sign, `[^@]`, identifes everything up to the `@` sign. The asterisk, `*`, identifies all instances of the preceding token. In this case, the `@` sign.

</td>
</tr>
<tr>
<td valign="top">

`(@)`

</td>
<td valign="top">

The second group identifies the `@` symbol

</td>
</tr>
<tr>
<td valign="top">

`([^.]*)`

</td>
<td valign="top">

The third group identifies the period between the domain and the domain extension. The `[^.]` identifies everything up to the period. The asterisk identifies all instances of the preceding token. In this case, the period.

</td>
</tr>
<tr>
<td valign="top">

\(.\*\)

</td>
<td valign="top">

The fourth group identifies the the content after the period.

</td>
</tr>
<tr>
<td valign="top">

`$`

</td>
<td valign="top">

The dollar sign `$` identifies the end of the string.

</td>
</tr>
</table>

Now, let's see how defining each group with a different variance type looks. The variance types work the same as the Pattern Variance options for Default, Character, Preserve, and String. The input address, `stephanie.milkowski@business.com`, becomes `linqqltco.tcsdxoldc@ABC.jmz` with the these settings.


<table>
<tr>
<th valign="top">

Group Number

</th>
<th valign="top">

Variance Type

</th>
<th valign="top">

Value

</th>
<th valign="top">

Input and Output data

</th>
</tr>
<tr>
<td valign="top">

1

</td>
<td valign="top">

Character

</td>
<td valign="top">

a-z

</td>
<td valign="top">

Input: stephanie.milkowski

Output: linqqltco.tcsdxoldc

</td>
</tr>
<tr>
<td valign="top">

2

</td>
<td valign="top">

Preserve

</td>
<td valign="top">

n/a

</td>
<td valign="top">

@

</td>
</tr>
<tr>
<td valign="top">

3

</td>
<td valign="top">

String

</td>
<td valign="top">

ABC|123

</td>
<td valign="top">

ABC

</td>
</tr>
<tr>
<td valign="top">

4

</td>
<td valign="top">

Default

</td>
<td valign="top">

n/a

</td>
<td valign="top">

jmz

</td>
</tr>
</table>

Here is another example that changes `jon.gill@ai.com` to `fev.hesx@123.net` with these settings.


<table>
<tr>
<th valign="top">

Group Number

</th>
<th valign="top">

Variance Type

</th>
<th valign="top">

Value

</th>
<th valign="top">

Input and Output data

</th>
</tr>
<tr>
<td valign="top">

1

</td>
<td valign="top">

Character

</td>
<td valign="top">

a-z

</td>
<td valign="top">

Input: jon.gill

Output: fev.hesx

</td>
</tr>
<tr>
<td valign="top">

2

</td>
<td valign="top">

Preserve

</td>
<td valign="top">

n/a

</td>
<td valign="top">

@

</td>
</tr>
<tr>
<td valign="top">

3

</td>
<td valign="top">

String

</td>
<td valign="top">

ABC | 123

</td>
<td valign="top">

123

</td>
</tr>
<tr>
<td valign="top">

4

</td>
<td valign="top">

String

</td>
<td valign="top">

com | gov | net | org

</td>
<td valign="top">

net

</td>
</tr>
</table>

With Pattern Variance Regular Expression, you don't have to know the starting position or length of a piece of data. For those times when the data is of the same length and structure, you can use the Pattern Variance option.

