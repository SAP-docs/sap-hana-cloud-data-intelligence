<!-- loio1326d32702ae4ae892bdf8127bcdd845 -->

# Person and Firm Cleanse Output Columns

Map the output columns in the Person and Firm Cleanse node.



<a name="loio1326d32702ae4ae892bdf8127bcdd845__section_tpn_yrk_jkb"/>

## Person Cleansing Best Practices

When you set the *Data Type* option to *Person* and the *Cleanse* option to anything except *Global*, map the columns in a way that is appropriate for that region or country. When setting the *Cleanse* option to *Global*, follow these best practices:

-   When outputting to a single person column, map to the *Person* column.
-   When outputting to two columns \(first and last names\), map to *First Name and Middle Name* and *Last Name 1-2* columns.
-   When outputting to three columns \(first, middle, and last names\), map to *First Name*, *Middle Name*, and *Last Name 1-2* columns.
-   When outputting to four columns \(first, middle, paternal last, and maternal last names\), select *First Name*, *Middle Name*, *Last Name*, and *Last Name 2* columns.



## Output Columns

The columns are listed alphabetically. Some columns are available only in one of the following data types: Firm, Person, or Person and Firm. The Data Type column shows the data types where the column is available.


<table>
<tr>
<th valign="top">

Output Column

</th>
<th valign="top">

Description

</th>
<th valign="top">

Data Type

</th>
</tr>
<tr>
<td valign="top">

Extra

</td>
<td valign="top">

Data that is determined to be something other than organization or person name data.

</td>
<td valign="top">

Firm, Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Firm

</td>
<td valign="top">

The cleansed form of the organization name.

</td>
<td valign="top">

Firm, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

First Name

</td>
<td valign="top">

First given names for most cleanse domains. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the First Name is “John”. For some domains such as French, the First Name contains the first two given names when the person has a compound name. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the First Name is “John Paul”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

First Name and Middle Name

</td>
<td valign="top">

Combination of the First Name column and the Middle Name column. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the First Name and Middle Name is “John Paul”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Gender

</td>
<td valign="top">

Gender of the person as classified in the reference data and is based on the probability of gender within locales represented by the cleanse domain. The gender is determined primarily by the name prefix or first name and, when ambiguous, then by the middle name.

MALE\_STRONG and FEMALE\_STRONG are generated when the gender confidence is high.

MALE\_WEAK and FEMALE\_WEAK are generated when the gender confidence is medium.

AMBIGUOUS is generated when the gender confidence is low.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Honorary Postname

</td>
<td valign="top">

Name suffix that represents honorific or academic affiliation. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the Honorary Postname is “PhD”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Information Code

</td>
<td valign="top">

Code generated only for records that have data in the firm or person columns that appears to be suspect.

</td>
<td valign="top">

Firm, Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Last Name

</td>
<td valign="top">

The full last name for most cleanse domains, even when the last name consists of multiple last names. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the Last Name is “Anderson Schmidt”. For some domains such as Spanish and Portuguese, the Last Name contains only the first of the last names when the person has a compound last name. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the Last Name is “Anderson”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Last Name 1-2

</td>
<td valign="top">

Combination of the Last Name column and the Last Name 2 column. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the Last Name 1-2 is “Anderson Schmidt”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Last Name 2

</td>
<td valign="top">

This column is empty for most cleanse domains because it’s the Last Name column that contains the full last name when a last name consists of multiple names. For some domains such as Spanish and Portuguese, Last Name 2 contains the second of the last names when the person has a compound last name. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the Last Name 2 is “Schmidt”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Maturity Postname

</td>
<td valign="top">

Name suffix that represents generational level. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the Maturity Postname is “Jr.”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Middle Name

</td>
<td valign="top">

Second given name for most cleanse domains. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the Middle Name is “Paul”. For some domains such as French, when the person has a compound name the First Name contains the first two given names and the Middle Name is empty unless there is a third name. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the First Name is “John Paul” and the Middle Name is empty.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Name Designator

</td>
<td valign="top">

Designator that can be input with the person name. For example, in “Attn: John Anderson” the Name Designator is “Attn:”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Person

</td>
<td valign="top">

Full person name with the name suffix, but without the name prefix, name designator, or occupational title. For example, in “Mr. John Paul Anderson Schmidt Jr., PhD” the Person is “John Paul Anderson Schmidt Jr., PhD”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Person 2

</td>
<td valign="top">

Name of the second person when data is input with two person names. For example, in “John and Mary Anderson” the Person is “John Anderson” and the Person 2 is “Mary Anderson”, and in “Gurvinder Singh s/o Sh. Tejveer Singh” the Person is “Gurvinder Singh” and the Person 2 is “Tejveer Singh”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Person or Firm

</td>
<td valign="top">

A person name in some records and an organization name in other records. This column contains data only when a column is input mapped to Person or Firm, and is intended to be used when a single column may contain either a person name or an organization name. For example, a customer name column in which the customer may be an individual or a corporation.

</td>
<td valign="top">

Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Prename

</td>
<td valign="top">

Name prefix that can represent either a personal title such as “Mr.” or “Ms.” or a professional title such as “Dr.” or “Prof.”. For example, in “Mr. John Paul Anderson Schmidt Jr., Ph. D.” the Prename is “Mr.”.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
<tr>
<td valign="top">

Title

</td>
<td valign="top">

The job or occupational title of a person. For example, Manager or Vice President of Marketing.

</td>
<td valign="top">

Person, Person and Firm

</td>
</tr>
</table>

