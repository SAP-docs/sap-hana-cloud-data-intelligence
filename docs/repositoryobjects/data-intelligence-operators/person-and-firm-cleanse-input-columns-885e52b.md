<!-- loio885e52bcaf72418386b65efdf13d858e -->

# Person and Firm Cleanse Input Columns

Map the input columns in the Person and Firm Cleanse node.



<a name="loio885e52bcaf72418386b65efdf13d858e__section_wqc_xdr_jkb"/>

## Person Cleansing Best Practice

When you set the *Data Type* option to *Person* and the name is in a single input column, map it to *Person*. Otherwise, map the name input columns to the discrete input columns such as *First Name*, *Middle Name*, and *Last Name*. An error occurs if you attempt to map the input data to *Person* and other discrete input fields at the same time.



## Input Columns

The columns are listed alphabetically. Some columns are available only in one of the following data types: Firm, Person, or Person and Firm. The Data Type column shows the data types where the column is available.


<table>
<tr>
<th valign="top">

Input Column

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

Country

Language

Region

</td>
<td valign="top">

Use these columns to control how the data is processed and output on a record-by-record basis. You must prepare the content yourself before inputting to the Cleanse operator. To use this feature, Country is required, and Language and Region are optional.

*Country*: Prepare a column that contains the appropriate 2-character ISO country code. Country is the primary column that determines how the data is processed and output.

*Language*: This column is optional and when mapped it is used only when the country is Belgium \(BE\) or Switzerland \(CH\). For Belgium records, include FR for records that use the French domain and include NL for records that use the Dutch domain. For Switzerland records, include DE for records that use the German domain, include FR for records that use the French domain, and include IT for records that use the Italian domain. If nothing is mapped to Language, then the French domain is used for all Belgium records and the German domain is used for all Switzerland records.

*Region*: This column is optional and when mapped it is used only when the country is Canada \(CA\). For Canada records, include QC \(Quebec\) for records that use the French domain, and for records that use the English domain you can include a blank, null or any other 2-character province abbreviation. If nothing is mapped to Region, then the English \(EN\_US\) domain is used for all Canada records.

</td>
<td valign="top">

Firm, Person, Person or Firm

</td>
</tr>
<tr>
<td valign="top">

Firm

</td>
<td valign="top">

Map a discrete column that contains organization name information to this column. The contents of this column can include names of companies, organized groups, educational institutions, and so on.

Operator can parse only a single firm at a time. Additional firms can be parsed by adding a second operator to the workflow.

</td>
<td valign="top">

Firm

</td>
</tr>
<tr>
<td valign="top">

First Name

</td>
<td valign="top">

Map a discrete column that contains first name information to this column. The contents of this column can contain a combination of first name, middle name, compound names, or prenames.

</td>
<td valign="top">

Person

</td>
</tr>
<tr>
<td valign="top">

Honorary Postname

</td>
<td valign="top">

Map a discrete column that contains honorific name suffix information to this column. For example, Ph.D.

</td>
<td valign="top">

Person

</td>
</tr>
<tr>
<td valign="top">

Last Name

</td>
<td valign="top">

Map a discrete column that contains last name information to this column. The contents of this column can contain a single last name, compound last names, or name suffix information.

</td>
<td valign="top">

Person

</td>
</tr>
<tr>
<td valign="top">

Last Name 2

</td>
<td valign="top">

Map a discrete column that contains a second last name to this column. Map to this column only if the input data contains two last name columns. For example, map a paternal last name column to Last Name and map a maternal last name column to Last Name 2, or vice versa depending on cultural norms.

</td>
<td valign="top">

Person

</td>
</tr>
<tr>
<td valign="top">

Maturity Postname

</td>
<td valign="top">

Map a discrete column that contains maturity name suffix information to this column. For example, Jr., Sr., or III.

</td>
<td valign="top">

Person

</td>
</tr>
<tr>
<td valign="top">

Middle Name

</td>
<td valign="top">

Map a discrete column that contains middle name information to this column. Map to this column only if the input data contains two given name columns. For example, map a first name column to First Name and map a middle name column to Middle Name. If the input data contains only one column that contains the combination of first name and middle name, map the column to First Name; do not map any column to Middle Name.

</td>
<td valign="top">

Person

</td>
</tr>
<tr>
<td valign="top">

Person

</td>
<td valign="top">

Use this input field when the person information is in a single field. Eor example Mary Angela Smith.

</td>
<td valign="top">

Person

</td>
</tr>
<tr>
<td valign="top">

Person or Firm

</td>
<td valign="top">

Map a discrete column to this column that contains a person name in some records and an organization name in other records. For example, if there is a customer name column in which some customers are individuals and other customers are organizations.

</td>
<td valign="top">

Person or Firm

</td>
</tr>
<tr>
<td valign="top">

Prename

</td>
<td valign="top">

Map a discrete column that contains name prefix information to this column. For example, Mr., Mrs., Dr., or Lt. Col.

</td>
<td valign="top">

Person

</td>
</tr>
<tr>
<td valign="top">

Title

</td>
<td valign="top">

Map a discrete column that contains occupational title information to this column.

</td>
<td valign="top">

Person

</td>
</tr>
</table>

