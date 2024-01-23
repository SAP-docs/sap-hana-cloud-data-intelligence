<!-- loio2dbdce9e2271474e9c98a2948b14ec47 -->

# Anonymized Groups Example

Use anonymization to place masked data into match groups so that you can publish data without risking reidentification of sensitive data.

Before masking, the data might be unique. After masking several columns of identifying data with *Mask*, *Date Generalization*, or *Numeric Generalization*, there will be duplicate records. In the Anonymization settings, you can choose the minimum number of records you want to output in a group. The groups that contain fewer records than the number you specify are not output. The larger the number you enter \(from 2 through 100\), the less likely the data can be reidentified and a smaller number of records are output. The lower the number entered, the more likely the data can be reidentified and a larger number of records are output.

Let's say that you work for an insurance company. You want to publish quarterly information about the cause of emergency room visits without compromising the patients' privacy.


<table>
<tr>
<th valign="top">

Row ID

</th>
<th valign="top">

Patient ID

</th>
<th valign="top">

Name

</th>
<th valign="top">

Age

</th>
<th valign="top">

Postcode

</th>
<th valign="top">

Date of Visit

</th>
<th valign="top">

Issue

</th>
</tr>
<tr>
<td valign="top">

1

</td>
<td valign="top">

L1234-0987

</td>
<td valign="top">

James Smith

</td>
<td valign="top">

1

</td>
<td valign="top">

54601

</td>
<td valign="top">

05/13/2017

</td>
<td valign="top">

Ear infection

</td>
</tr>
<tr>
<td valign="top">

2

</td>
<td valign="top">

R5678-6543

</td>
<td valign="top">

Allison Zhou

</td>
<td valign="top">

26

</td>
<td valign="top">

54650

</td>
<td valign="top">

02/06/2017

</td>
<td valign="top">

Influenza

</td>
</tr>
<tr>
<td valign="top">

3

</td>
<td valign="top">

J2345-9876

</td>
<td valign="top">

Mia Vang

</td>
<td valign="top">

53

</td>
<td valign="top">

55190

</td>
<td valign="top">

12/18/2016

</td>
<td valign="top">

Heart attack

</td>
</tr>
<tr>
<td valign="top">

4

</td>
<td valign="top">

J6789-5432

</td>
<td valign="top">

Ben McCleary

</td>
<td valign="top">

68

</td>
<td valign="top">

55118

</td>
<td valign="top">

09/25/2016

</td>
<td valign="top">

Stroke

</td>
</tr>
<tr>
<td valign="top">

5

</td>
<td valign="top">

P7789-1212

</td>
<td valign="top">

Franz Gullikson

</td>
<td valign="top">

2

</td>
<td valign="top">

54603

</td>
<td valign="top">

04/15/2017

</td>
<td valign="top">

Ear infection

</td>
</tr>
<tr>
<td valign="top">

6

</td>
<td valign="top">

R0606-1223

</td>
<td valign="top">

Joseph Kaswizki

</td>
<td valign="top">

4

</td>
<td valign="top">

54551

</td>
<td valign="top">

01/21/2017

</td>
<td valign="top">

Influenza

</td>
</tr>
<tr>
<td valign="top">

7

</td>
<td valign="top">

B7212-7306

</td>
<td valign="top">

Avijit Farooq

</td>
<td valign="top">

3

</td>
<td valign="top">

54601

</td>
<td valign="top">

02/02/2017

</td>
<td valign="top">

Influenza

</td>
</tr>
<tr>
<td valign="top">

8

</td>
<td valign="top">

R8675-3099

</td>
<td valign="top">

Alejandro Rodriquez

</td>
<td valign="top">

18

</td>
<td valign="top">

54650

</td>
<td valign="top">

11/27/2016

</td>
<td valign="top">

Concussion

</td>
</tr>
<tr>
<td valign="top">

9

</td>
<td valign="top">

J0673-1272

</td>
<td valign="top">

Aleksandra Kaminski

</td>
<td valign="top">

2

</td>
<td valign="top">

54603

</td>
<td valign="top">

04/17/2017

</td>
<td valign="top">

Ear infection

</td>
</tr>
<tr>
<td valign="top">

10

</td>
<td valign="top">

W1720-0825

</td>
<td valign="top">

Amanda Barns

</td>
<td valign="top">

4

</td>
<td valign="top">

54601

</td>
<td valign="top">

02/04/2017

</td>
<td valign="top">

Influenza

</td>
</tr>
</table>

You can mask the data in many different ways. This table shows how we’ve defined each of the columns.


<table>
<tr>
<th valign="top">

Column Name

</th>
<th valign="top">

Column Designation

</th>
</tr>
<tr>
<td valign="top">

Row ID

</td>
<td valign="top">

Nonsensitive

</td>
</tr>
<tr>
<td valign="top">

Patient ID

</td>
<td valign="top">

Identifier

</td>
</tr>
<tr>
<td valign="top">

Name

</td>
<td valign="top">

Identifier

</td>
</tr>
<tr>
<td valign="top">

Age

</td>
<td valign="top">

Quasi-identifier

Operation: Numeric Generalization

-   Minimum Value: 13
-   Minimum Value Inclusive: True
-   Maximum Value: 19
-   Maximum Value Inclusive: True
-   Replacement Value: Teenager
-   Default Replacement Value: other

> ### Note:  
> Create more groups, defining ranges such as 0-5, 6-12, 20-29, 30-39, and so on.



</td>
</tr>
<tr>
<td valign="top">

Postcode

</td>
<td valign="top">

Quasi-identifier

Operation: Mask

-   Starting Position: Start
-   Unmasked Length: 2
-   Masking Character: \*
-   Maintain Formatting: False



</td>
</tr>
<tr>
<td valign="top">

Date of Visit

</td>
<td valign="top">

Quasi-identifier

Operation: Date Generalization

Auto Range Scale: Not\_In\_Use

Date Generalization Range Definition:

-   First range:
    -   Minimum Date: 01/01/2017
    -   Minimum Date Inclusive: True
    -   Maximum Date: 03/31/2017
    -   Maximum Date Inclusive: True
    -   Replacement Value: Q1 2017


-   Second range:
    -   Minimum Date: 04/01/2017
    -   Minimum Date Inclusive: True
    -   Maximum Date: 06/30/2017
    -   Maximum Date Inclusive: True
    -   Replacement Value: Q2 2017

-   Third range:
    -   Minimum Date: 07/01/2017
    -   Minimum Date Inclusive: True
    -   Maximum Date: 09/30/2017
    -   Maximum Date Inclusive: True
    -   Replacement Value: Q3 2017

-   Fourth range:
    -   Minimum Date: 10/01/2017
    -   Minimum Date Inclusive: True
    -   Maximum Date: 12/31/2017
    -   Maximum Date Inclusive: True
    -   Replacement Value: Q4 2017


Default Replacement Value: Other

</td>
</tr>
<tr>
<td valign="top">

Issue

</td>
<td valign="top">

Sensitive

</td>
</tr>
</table>

In this example, we removed the patient name and ID. We masked the last three digits of the postcode. We generalized the age and generalized the date of service from a specific day into a generalized quarter. We defined the Issue column as Sensitive. The resulting data set shows how the formerly unique records are more generic while still providing the necessary data.


<table>
<tr>
<th valign="top">

Row ID

</th>
<th valign="top">

Age

</th>
<th valign="top">

Postcode

</th>
<th valign="top">

Date of Visit

</th>
<th valign="top">

Issue

</th>
</tr>
<tr>
<td valign="top">

1

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q2 2017

</td>
<td valign="top">

Ear infection

</td>
</tr>
<tr>
<td valign="top">

2

</td>
<td valign="top">

\[20-29\]

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q1 2017

</td>
<td valign="top">

Influenza

</td>
</tr>
<tr>
<td valign="top">

3

</td>
<td valign="top">

\[50-59\]

</td>
<td valign="top">

55\*\*\*

</td>
<td valign="top">

Q4 2016

</td>
<td valign="top">

Heart attack

</td>
</tr>
<tr>
<td valign="top">

4

</td>
<td valign="top">

\[60-69\]

</td>
<td valign="top">

55\*\*\*

</td>
<td valign="top">

Q3 2016

</td>
<td valign="top">

Stroke

</td>
</tr>
<tr>
<td valign="top">

5

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q2 2017

</td>
<td valign="top">

Ear infection

</td>
</tr>
<tr>
<td valign="top">

6

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q1 2017

</td>
<td valign="top">

Influenza

</td>
</tr>
<tr>
<td valign="top">

7

</td>
<td valign="top">

\[0-5\]

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q1 2017

</td>
<td valign="top">

Influenza

</td>
</tr>
<tr>
<td valign="top">

8

</td>
<td valign="top">

Teenager

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q4 2016

</td>
<td valign="top">

Concussion

</td>
</tr>
<tr>
<td valign="top">

9

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q2 2017

</td>
<td valign="top">

Ear infection

</td>
</tr>
<tr>
<td valign="top">

10

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q1 2017

</td>
<td valign="top">

Influenza

</td>
</tr>
</table>

Now that the data is masked, you can see how the data is placed into anonymized groups.


<table>
<tr>
<th valign="top">

Age

</th>
<th valign="top">

Postcode

</th>
<th valign="top">

Date of Visit

</th>
<th valign="top">

Issue

</th>
<th valign="top">

Anonymization Group Size

</th>
</tr>
<tr>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q1 2017

</td>
<td valign="top">

Influenza

</td>
<td valign="top">

3

</td>
</tr>
<tr>
<td valign="top">

\[20-29\]

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q1 2017

</td>
<td valign="top">

Influenza

</td>
<td valign="top">

1

</td>
</tr>
<tr>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q2 2017

</td>
<td valign="top">

Ear Infection

</td>
<td valign="top">

3

</td>
</tr>
<tr>
<td valign="top">

\[50-59\]

</td>
<td valign="top">

55\*\*\*

</td>
<td valign="top">

Q4 2016

</td>
<td valign="top">

Heart attack

</td>
<td valign="top">

1

</td>
</tr>
<tr>
<td valign="top">

\[60-69\]

</td>
<td valign="top">

55\*\*\*

</td>
<td valign="top">

Q3 2016

</td>
<td valign="top">

Stroke

</td>
<td valign="top">

1

</td>
</tr>
<tr>
<td valign="top">

Teenager

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q4 2016

</td>
<td valign="top">

Concussion

</td>
<td valign="top">

1

</td>
</tr>
</table>

If you set the *Minimum rows in anonymized group* option to 3, then you could publish six of 10 records.


<table>
<tr>
<th valign="top">

Row ID

</th>
<th valign="top">

Age

</th>
<th valign="top">

Postcode

</th>
<th valign="top">

Date of Visit

</th>
<th valign="top">

Issue

</th>
</tr>
<tr>
<td valign="top">

1

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q2 2017

</td>
<td valign="top">

Ear infection

</td>
</tr>
<tr>
<td valign="top">

5

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q2 2017

</td>
<td valign="top">

Ear infection

</td>
</tr>
<tr>
<td valign="top">

6

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q1 2017

</td>
<td valign="top">

Influenza

</td>
</tr>
<tr>
<td valign="top">

7

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q1 2017

</td>
<td valign="top">

Influenza

</td>
</tr>
<tr>
<td valign="top">

9

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q2 2017

</td>
<td valign="top">

Ear infection

</td>
</tr>
<tr>
<td valign="top">

10

</td>
<td valign="top">

Toddler

</td>
<td valign="top">

54\*\*\*

</td>
<td valign="top">

Q1 2017

</td>
<td valign="top">

Influenza

</td>
</tr>
</table>

Now, let's say that the issue in the first row is a concussion rather than an ear infection. Would the record still be published? Yes, because the Issue column isn’t anonymized. The Age, Postcode, and Date of Visit columns are the only anonymized columns. Therefore, only the data in those columns are used in forming anonymized groups, not the data in the Issue column.

When the operator receives more data, those groups that previously did not have enough records to output may reach the minimum value, and then are output. Any records meeting the criteria of other output groups are immediately added to those groups.

If you would like to use the data in the Issue column for securing your data in addition to the masking and generalizations, you can set the *l-Diverstiy* or *t-Closeness* options.



<a name="loio2dbdce9e2271474e9c98a2948b14ec47__section_w1b_4g4_3gb"/>

## Using the l-Diversity Option

To make equivalency classes more secure, you can set the *Distinct l-Diversity* option. This option defines a minimum number of distinct values that must be present, or the equivalency class is not output.

The *l-Diversity* option works with columns that have the *Column Designation* set to *Sensitive*. After selecting the *Distinct l-Diversity* option, set the *l-Value* to a positive value from 2 through 100. Only those equivalency classes that meet this minimum value are output.

Building on the previous example, the Issue column is the only column defined as *Sensitive*. There are two distinct values in the equivalency class: Ear Infection and Influenza. If you set the *l-Value* to 2, then this equivalency class is output. If you set this option to 3 or more, then it is not output because there aren’t enough distinct values in the equivalency class.



<a name="loio2dbdce9e2271474e9c98a2948b14ec47__section_fqv_nf5_y3b"/>

## Using the t-Closeness Option

You can use the *t-Closeness* option with the *l-Diversity* option. The *l-Diversity* option ensures that there are a certain number of similar records in an equivalency class. The *t-Closeness* option defines how closely the sensitive values in the equivalency class match the distribution of sensitive values in the source table.

Let's say that your equivalency class has 100 records in it. Let's also say that 60% of the records in the source table have an influenza issue. Setting the *t-Value* close to 0.000001 places approximately 60 influenza records in the equivalency class. If you set the *t-Value* close to 1.0, then there’s a less equal distribution in the equivalency class relative to the source table.

