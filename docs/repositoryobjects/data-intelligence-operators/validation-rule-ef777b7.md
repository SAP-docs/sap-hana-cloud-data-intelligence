<!-- loioef777b793aa44845807e387b28c3eea0 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Validation Rule

Create rules and route records that pass through the Pass output port. Route failed records through the Fail output port.



You may want to create a validation rule to output a list of users who are the age of 18 or older, for example. You can create a rule that specifies the AGE column is \>= \(greater than or equal to\) 18. Any values that are 18 or more are output through the Pass port, while those records that are less than 18 or have a null or invalid value are output through the Fail port.

You can view defined examples of this operator by clicking the Graphs tab and searching for "Basic Validation" and "IoT Validation".



<a name="loioef777b793aa44845807e387b28c3eea0__section_sq1_nf3_vdb"/>

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

string

</td>
<td valign="top">

Required. Enter the name of the validation rule operator.

</td>
</tr>
<tr>
<td valign="top">

Rules

</td>
<td valign="top">

array

</td>
<td valign="top">

Required: Enter one or more rules. Click the Open Editor icon, and then click *\+Add item* and complete the following options.

-   **Column** \(type string\): Required. Enter the column name. For example, AGE.
-   **Condition** \(type string\): Required. Enter the condition. For example, \>=. The following conditions are available:
    -   IS NULL
    -   IS NOT NULL
    -   <
    -   <=
    -   =
    -   <\>

        In the expression `Title <> 'CEO'`, the values CEO and null fail the rule.

    -   =
    -   LIKE

        When using LIKE, remember these items:

        -   STRING matches any STRING matching expression, which must be in single quotes. For example 'Be%' matches Ben, Bench, Begin.
        -   INTEGER matches any INTEGER specified without single quotes, or a single quoted expression such as '15%', which matches values of 15, 150, 151, and so on.
        -   NUMBER matches any INTEGER or NUMBER.
        -   Use these wildcards with LIKE;
            -   %: A string of zero or more characters.
            -   \_ \(underscore\): A single character.
            -   \[\]: A single character with a specific range or set.
            -   \[^\]: A single character not within the specified range or set.


    -   MATCH PATTERN: Enter a pattern based on the match\_pattern function.
    -   BETWEEN: Specify a range of values.

        When using BEWEEN, remember these items:

        -   The values set are inclusive. For example, `[20, 22]` includes 4 values: 20, 21, and 22.
        -   Enclose string values in single quotes.
        -   STRING `['A', 'D']` matches any STRING alphabetically, inclusively between A and D.
        -   INTEGER `[20,24]` matches any INTEGER, NUMBER, or STRING, inclusively between 20 and 24.
        -   NUMBER `[20.15, 400.78]` matches any INTEGER or NUMBER, inclusively between 20.15 and 400.78.

    -   IN SET
    -   CUSTOM: Select to call a more complex function that is defined in the Validation Functions option.

-   **Value** \(type string\): Required. See Value list.
-   **Value List** \(type string\): Required. Depending on the condition you selected, you may need to enter a value or a values list.

    For example, enter a value of 18. A values list is available when you select BETWEEN or IN SET. Click *\+Add item* to set the minimum value, for example, 9. Click *\+Add* item again to set the maximum value, for example, 17. If the substitution value is a hardcoded string you must enclose the string in single quotes.

    If single quotes are present within the string then those must be escaped with a backslash \(\) character.

-   **Fail Action** \(type string\): Enter the Fail Action for those records that do not pass the rule.
    -   Fail: Sends the record to the Fail port.
    -   Pass: Sends the record to the Pass port.
    -   Both: Sends the record to the Pass and Fail ports.




</td>
</tr>
<tr>
<td valign="top">

Substitutions

</td>
<td valign="top">

array

</td>
<td valign="top">

If you choose Pass or Both for a rule's Fail Action, you can enter a substitution value for the failed values that go to the Pass port. For example, if you have a rule that the column AGE Is Not Null, you can create a substitution variable that assigns the AGE column with a value of 999.

Therefore, the failed records are output to both the Fail and Pass ports. The failed records included in the Pass port have an age of 999, whereas the same records in the failed port continue to have a null value.

If the substitution value is a hardcoded string, you must enclose the string in single quotes. If single quotes are present within the string, then those quotes must be escaped with a backslash \(\\\) character.

</td>
</tr>
<tr>
<td valign="top">

Validation Functions

</td>
<td valign="top">

array

</td>
<td valign="top">

If you want to create a more complex function, click the *Open Editor* icon, and then click *\+Add item* and complete the following options:

1.  Enter the name of the function. For example, `EighteenAndOlder`.
2.  Enter the function in the *Body* option. For example, `if($arg >= 18) return 1; else return 0;.` This function reads: if the argument passed is greater than or equal to 18, return a 1 \(true\). If the value is less than 18, then return 0 \(false\).
3.  Click *\+Add item* to create the arguments.
4.  Enter the name of the argument. For example, `$arg`.
5.  Define the data type of the argument: *String*, *Number*, or *Integer*.
6.  If you chose a *String* data type, then enter the *Length*. For example, `256`.
7.  Click *Save*.
8.  In the *Rules* option, set the *Condition* to *CUSTOM*. In the *Value* option, call the name of the validation function. For example, `EighteenAndOlder(AGE)`. Note that the 'AGE' in parentheses is the name of the input column name from your defined schema. Make sure that the input column's data type in the schema matches the data type defined in this argument.
9.  Click `Save`.



</td>
</tr>
<tr>
<td valign="top">

Input Schema

</td>
<td valign="top">

array

</td>
<td valign="top">

Required. Define the column names and data types for the input source used in the Validation Rule operator. Click the *Open Editor* icon, and then click *\+Add item* for each input column. If you have FIRST\_NAME, LAST\_NAME, and AGE, you would create three values.

1.  Enter the name of the first column.
2.  Select the data type.
3.  If you chose a *String* data type, then enter the *Length*. For example, `256`.
4.  Repeat for the additional columns, and then click *Save*.



</td>
</tr>
<tr>
<td valign="top">

Format

</td>
<td valign="top">

string

</td>
<td valign="top">

Required. Choose the format of the input.

</td>
</tr>
<tr>
<td valign="top">

CSV Properties

</td>
<td valign="top">

array

</td>
<td valign="top">

Optional. Click the :pencil2:icon, and then set these options.

-   Column Delimiter \(type string\): The field separator. Only the following characters are supported: , ; | : and TAB.

    Default: ,

-   Text Delimiter Style \(type string\): Indicates how the text delimiter should be applied. If Always is selected, all columns will have a text delimiter; if Minimal, the text delimiter will be added only when required. The text delimiter style is used to correctly format the output data.
-   Header Included \(type boolean\): Indicates that the output will have header information. The input schema is used to set the first row of the output as header. If the input file contains header information, preprocess the data by removing the header and sending it to the Validation Rule.



</td>
</tr>
<tr>
<td valign="top">

Batch Size

</td>
<td valign="top">

integer

</td>
<td valign="top">

Required. Enter the number of rows you want included in each batch that is output from this operator. If you have 1000 rows of data and set this option to 250, then four batches are output. If you want all the records output in a single batch, set the size larger than the greatest input size. In the previous example, you would set this option to 1001 or higher.

</td>
</tr>
</table>



<a name="loioef777b793aa44845807e387b28c3eea0__section_knq_5f3_vdb"/>

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

string

</td>
<td valign="top">

The input port to the Validation Rule operator expects the data in the format specified by the Format option.

</td>
</tr>
</table>



<a name="loioef777b793aa44845807e387b28c3eea0__section_swc_cg3_vdb"/>

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

`pass`

</td>
<td valign="top">

string

</td>
<td valign="top">

Contains the list of passed records. It shows the contents of each column. If a substitution variable was used on the failed records, then that value is included in the column that was defined.

</td>
</tr>
<tr>
<td valign="top">

`fail`

</td>
<td valign="top">

string

</td>
<td valign="top">

Contains the list of records that failed the rule or rules. Each record has the columns, the Failed Action indicator \(B=Both, F=Fail\), and which rules the record failed.

</td>
</tr>
<tr>
<td valign="top">

`failInformation`

</td>
<td valign="top">

string

</td>
<td valign="top">

Contains information about why the record failed. It contains a unique ID for each record, the name of the rule that failed, and the column name.

</td>
</tr>
<tr>
<td valign="top">

`outError`

</td>
<td valign="top">

string

</td>
<td valign="top">

When mapped, the operator error is sent to next operator in line, and the graph is run. When not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

