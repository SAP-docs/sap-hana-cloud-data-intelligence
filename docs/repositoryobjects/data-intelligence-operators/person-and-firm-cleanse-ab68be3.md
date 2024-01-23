<!-- loioab68be3bfd9543e69a855810f6d84f29 -->

# Person and Firm Cleanse

The Person and Firm Cleanse operator identifies the names of people and firms even when both types of names are in the same column.



> ### Note:  
> This operator is deprecated.

Sometimes person and firm \(business organization\) data is listed in one column, such as a Customer column. Let's say that you own a bakery. You deliver your baked goods to businesses such as grocery stores as well as to people in their homes. In your data, you have a Customer column that contains both the names of businesses and of individual people.

In some instances, businesses have names that resemble peoples' names. For example, a person can be named Misty Green, but that can also be the name of a plant or an agricultural watering company.

Whether the person or firm data is in a single column or in separate person and firm columns, the Person and Firm Cleanse operator can help differentiate these types of data by comparing the name to a list of firm name data.



<a name="loioab68be3bfd9543e69a855810f6d84f29__section_zqr_3jt_hkb"/>

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

Cleanse

</td>
<td valign="top">

cleanse

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. When a country field is input to the Person and Firm Cleanse operator, then the person, title, firm, and person-or-firm data is cleansed according to regional standards of the input country. Use this setting to select which language or region domain you want to use by default when cleansing data for records that have a blank country or for all records when a country field is not available.

The Global domain is a special content domain that contains all variations and their associated properties. If a variation is not associated with domain-specific information, the Global domain serves as the default domain.

Default: "EN\_US - English \(United States & Canada\)"

</td>
</tr>
<tr>
<td valign="top">

Output

</td>
<td valign="top">

 

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory.

ertain output fields and formatting options are automatically set according to regional standards, based on the selected output format. When a country field is input to the Person or Firm Cleanse operator, then the person, title, firm, and person-or-firm data is output according to regional standards of the input country. Use this setting to select the cultural domain you want to use by default when cleansing data for records that have a blank country, or for all records when a country field isn't available.

For example, when selecting one of the English domains, if you output person name data to discrete fields, the first name is output to First Name, the middle name to Middle Name, and the full last name to Last Name \(nothing is output to Last Name 2\), and if you output to the composite Person field, the name is ordered as first name - middle name - last name - maturity postname - honorary postname with a space between each word.


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Output

</th>
</tr>
<tr>
<td valign="top">

Juan Carlos Sánchez Cruz Jr. PhD

</td>
<td valign="top">

Discrete field output:

-   First Name: Juan
-   Middle Name: Carlos
-   Last Name: Sánchez Cruz
-   Last Name2: n/a
-   Maturity Postname: Jr.
-   Honorary Postname: PhD



</td>
</tr>
<tr>
<td valign="top">

 

</td>
<td valign="top">

Composite field output:

Person: Juan Carlos Sánchez Cruz Jr. PhD

</td>
</tr>
</table>

When selecting one of the Spanish domains to output to discrete fields, the system outputs the paternal last name to Last Name and the maternal last name to Last Name 2.


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Output

</th>
</tr>
<tr>
<td valign="top">

Juan Carlos Sánchez Cruz Jr. PhD

</td>
<td valign="top">

Discrete field output:

-   First Name: Juan
-   Middle Name: Carlos
-   Last Name: Sánchez
-   Last Name2: Cruz
-   Maturity Postname: Jr.
-   Honorary Postname: PhD



</td>
</tr>
</table>

When selecting the Chinese domain, if you output to discrete fields, the system outputs the given name to First Name and the family name to Last Name. Nothing is output to Middle Name or Last Name 2. If you output to the composite Person field, the name is ordered as last name - first name without any spaces between the words.


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Output

</th>
</tr>
<tr>
<td valign="top">

Mie Ping Chen MD

</td>
<td valign="top">

Discrete field output:

-   First Name: Mie Ping
-   Middle Name: n/a
-   Last Name: Chen
-   Last Name2: n/a
-   Maturity Postname: n/a
-   Honorary Postname: MD



</td>
</tr>
<tr>
<td valign="top">

 

</td>
<td valign="top">

Composite field output:

Person: Chen Mie Ping MD

</td>
</tr>
</table>

The valid values are the same as Cleanse Domain, but you can select one domain only, and Global is not an option.

Default: "EN\_US - English \(United States & Canada\)"

</td>
</tr>
<tr>
<td valign="top">

Casing

</td>
<td valign="top">

 

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory: Specifies the casing format.

-   Mixed Case: Converts data to initial capitals. For example, if the input data is JOHN MCKAY, then the data is output as John McKay.

    > ### Note:  
    > The application intelligently capitalizes common names with mixed casing like McHenry, and MacKenzie. Also note that the mixed case option does not apply to email addresses.

-   Upper Case: Converts the casing to upper case. For example, JOHN MCKAY.

Default: "mixed"

</td>
</tr>
<tr>
<td valign="top">

Diacritics

</td>
<td valign="top">

diacritics

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Specifies whether to retain diacritical characters in the output:

-   Include: Retains the standardized diacritical characters. For example, Sánchez.
-   Remove: Replaces diacritical characters such as accent marks, umlauts, and so on, with the ASCII-equivalent letters. For example, Sanchez.

Default: "include"

</td>
</tr>
<tr>
<td valign="top">

Data Type

</td>
<td valign="top">

dataType

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Used to specify the type of parsing.

-   Firm: Contains only firm data
-   Person: Contains only person data
-   Person or Firm: Contains a mix of person and firm data

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Passthrough

</td>
<td valign="top">

passthrough

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Mandatory. Setting this option to True passes the input data unchanged to the output data. You cannot rename the input fields. If an input field has the same name as an output field defined in the operator, then the output field overwrites the input field's value.

false

</td>
</tr>
<tr>
<td valign="top">

\[Firm | Person | Person or Firm\] Input

</td>
<td valign="top">

 

</td>
<td valign="top">

Array

</td>
<td valign="top">

Click *\+ Add* to define one or more input columns where you specify the column name and mapping for each column.

</td>
</tr>
<tr>
<td valign="top">

Column ID

</td>
<td valign="top">

 

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. This string uniquely identifies the column and should match the ID or name of the column coming into the operator.

</td>
</tr>
<tr>
<td valign="top">

Mapping

</td>
<td valign="top">

 

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Specifies the mapping for this column.

</td>
</tr>
<tr>
<td valign="top">

\[Firm | Person | Person or Firm\] Input

</td>
<td valign="top">

 

</td>
<td valign="top">

Array

</td>
<td valign="top">

Mandatory. Click *\+ Add* to map from the internal processing columns to one or more output columns.

</td>
</tr>
<tr>
<td valign="top">

Column ID

</td>
<td valign="top">

 

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Name to give to the output column.

</td>
</tr>
<tr>
<td valign="top">

Mapping

</td>
<td valign="top">

 

</td>
<td valign="top">

String

</td>
<td valign="top">

Mandatory. Specifies the mapping to the output column.

</td>
</tr>
</table>

-   **[Person and Firm Cleanse Input Columns](person-and-firm-cleanse-input-columns-885e52b.md "Map the input columns in the Person and Firm Cleanse node.")**  
Map the input columns in the Person and Firm Cleanse node.
-   **[Person and Firm Cleanse Output Columns](person-and-firm-cleanse-output-columns-1326d32.md "Map the output columns in the Person and Firm Cleanse node.")**  
Map the output columns in the Person and Firm Cleanse node.

