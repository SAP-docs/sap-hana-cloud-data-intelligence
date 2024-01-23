<!-- loiocec2a76703104886a69ed5c90927f4a5 -->

# Validation Rule V2

Route records to Pass or Failed output ports based on a set of rules. Supported in Generation 2 graphs.



You may want to create a validation rule to output a list of users who are over the age of 18, for example. You can create a rule that specifies the AGE column is \>= \(greater than or equal to\) 18. Any values that are 18 or more are output through the ‘pass’ port, while those records that are less than 17 or have a null or invalid value are output through the ‘fail’ port. Likewise, you could have a dataset that contains invalid or incomplete data. Those invalid or incomplete records can be moved to a separate table to be corrected while the valid and complete data can pass to a table where the data can be used elsewhere in the business.

There are two ways of configuring the operator:

-   Create the rules in the Validation Rule operator.
-   Create the rules and rule bindings in a rulebook in the Metadata Explorer, and then reuse the rules by calling the rulebook ID in this operator.

    > ### Note:  
    > Rules can be mapped to one dataset only in the Metadata Explorer so that it matches the input pipe of this operator.
    > 
    > Only rulebooks with a type of graph \(rather than a standard rulebook\) can be used.


You can view defined examples of this operator by clicking the Graphs tab and searching for “Basic Validation”.



<a name="loiocec2a76703104886a69ed5c90927f4a5__section_sq1_nf3_vdb"/>

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

Rules Configuration

</td>
<td valign="top">

string

</td>
<td valign="top">

Required. Specifies the type of configuration:

-   Inline Rule Configuration: Create the rules in this operator.
-   Metadata Explorer Rulebook Configuration: Create the rules and map them to a dataset in a rulebook in the Metadata Explorer, and then call the rulebook ID in this operator.



</td>
</tr>
</table>

This option is available when *Rules Configuration* is set to *Metadata Explorer Rulebook Configuration*.


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

Rulebook ID

</td>
<td valign="top">

string

</td>
<td valign="top">

The available graph rulebooks are shown.

</td>
</tr>
</table>

These options are available when *Rules Configuration* is set to *Inline Rule Configuration*.


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

Rules

</td>
<td valign="top">

array

</td>
<td valign="top">

Enter one or more rules. Click the Pencil icon, and then click is set to Metadata Explorer Rulebook. Specifies the Metadata Explorer rulebook ID. The list of available graph rulebooks is shown.*\+Add* and complete the following options.

-   **Column** \(type string\): Required. Enter the column name. For example, AGE.
-   **Condition** is set to Metadata Explorer Rulebook. Specifies the Metadata Explorer rulebook \(type string\): Required. Enter the condition. For example, \>=. The following conditions are available:
    -   IS NULL
    -   IS NOT NULL
    -   <
    -   \>
    -   <=
    -   \>=
    -   =
    -   <\>

        In the expression `Title <> 'CEO'`, the values CEO and null fail the rule.

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

    For example, enter a value of 18. A values list is available when you select BETWEEN or IN SET. Click *\+Add item* to set the minimum value, for example, 9. Click *\+Add* item again to set the maximum value, for example, 17. If the substitution value is a hardcoded string, you must enclose the string in single quotes.

    If single quotes are present within the string, then those quotes must be escaped with a backslash \(\) character.

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

Therefore, the failed records are output to both the Fail and Pass ports. The failed records included in the Pass port have an age of 999, but the same records in the failed port continue to have a null value.

Click the Pencil icon, and then click the + Add icon and complete the following options.

-   Column: Enter the name of the column where you want to create a substitution.
-   Value: Enter a value for the substitution. If the substitution is a hardcoded string, then you must enclose the string in single quotes. If single quotes are present within the string, then those quotes must be escaped with a backslash \(\\\) character.



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

If you want to create a more complex function, click the Pencil icon, then click *\+Add item*, and then complete the following options:

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
</table>

In the Rules option, set the Condition to CUSTOM. In the Value option, call the name of the validation function. For example, EighteenAndOlder\(AGE\). Note that the ‘AGE’ in parentheses is the name of the input column name from your defined schema. Make sure that the input column’s data type in the schema matches the data type defined in this argument.



<a name="loiocec2a76703104886a69ed5c90927f4a5__section_knq_5f3_vdb"/>

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

input

</td>
<td valign="top">

table

</td>
<td valign="top">

Accepts table type input from an operator that generates vtype tables.

</td>
</tr>
</table>



<a name="loiocec2a76703104886a69ed5c90927f4a5__section_swc_cg3_vdb"/>

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

pass

</td>
<td valign="top">

table

</td>
<td valign="top">

The vtype-ID from the operator's input port is propagated. Contains the list of passed records. It shows the contents of each column. If a substitution variable was used on the failed records, then that value is included in the column that was defined.

</td>
</tr>
<tr>
<td valign="top">

fail

</td>
<td valign="top">

table

</td>
<td valign="top">

A new vtype-ID definition is generated, consisting of all of the columns from the input port and additional three columns:

ROW\_ID \(integer\),

ERROR\_ACTION \(string with length 1\),

ERROR\_COLUMNS \(string with length 500\)

Contains the list of failed records. Each record has the columns, the Failed Action indicator \(B=Both, F=Fail\), and which rules the record failed.

</td>
</tr>
<tr>
<td valign="top">

failInformation

</td>
<td valign="top">

table

</td>
<td valign="top">

Contains information about why the record failed. It contains a unique ID for each record, the name of the rule that failed, and the column name.

</td>
</tr>
</table>

> ### Note:  
> The output ports automatically generate the correct vtype-ID values that can be used by downstream operators.

