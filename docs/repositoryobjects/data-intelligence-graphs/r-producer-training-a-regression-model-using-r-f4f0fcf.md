<!-- loiof4f0fcf8d18e4b0f963525c74eea05b9 -->

# R Producer - Training a regression model using R



This graph consumes data from a CSV file stored in the Local File System \(vrep\) to create a linear regression model using the `lm` function.



In this example, we use the Boston Housing dataset to train a model in order to predict the median value of owner-occupied homes in thousands of dollars.



<a name="loiof4f0fcf8d18e4b0f963525c74eea05b9__section_n2m_5hy_2lb"/>

## Prerequisites

A CSV file stored in vrep with columns separated by semicolon \(';'\).



<a name="loiof4f0fcf8d18e4b0f963525c74eea05b9__section_cvt_jdy_2lb"/>

## Configure and Run the Graph

1.  In your ML scenario, go to the *Pipelines* tab;

2.  Choose *Create* to create a new pipeline;

3.  Input a new name for your pipeline and select the *R Producer Regression Example* from the drop-down list;

4.  Choose *Create*;

5.  Find your pipeline on the list and select the *Deploy* button;

6.  Optional: write a deployment description;

7.  On the *Previous Configurations* screen, choose the*Step 4* button to go to next configuration step;

8.  On *Pipeline Parameters*, write a new name for your model in the `NewArtifactName` field; and choose *Save*;

9.  Execute your graph.



<a name="loiof4f0fcf8d18e4b0f963525c74eea05b9__section_ksf_s3y_2lb"/>

## Training Operator



### Ports

-   Input

    -   Input: A message type with all file information provided by the Read File operator.


-   Output

    -   metrics: Model artifact to be saved;

    -   modelBlob: Model metrics.





### Dataset

The following is a sample of the CSV file with Boston Housing dataset. It is assumed that the target values are provided in the last column.

****


<table>
<tr>
<th valign="top">

crim

</th>
<th valign="top">

zn

</th>
<th valign="top">

indus

</th>
<th valign="top">

chas

</th>
<th valign="top">

nox

</th>
<th valign="top">

rm

</th>
<th valign="top">

age

</th>
<th valign="top">

dis

</th>
<th valign="top">

rad

</th>
<th valign="top">

tax

</th>
<th valign="top">

ptratio

</th>
<th valign="top">

black

</th>
<th valign="top">

lstat

</th>
<th valign="top">

mdev

</th>
</tr>
<tr>
<td valign="top">

0.00632

</td>
<td valign="top">

18

</td>
<td valign="top">

2.31

</td>
<td valign="top">

0

</td>
<td valign="top">

0.538

</td>
<td valign="top">

6.575

</td>
<td valign="top">

65.2

</td>
<td valign="top">

4.09

</td>
<td valign="top">

1

</td>
<td valign="top">

296

</td>
<td valign="top">

15.3

</td>
<td valign="top">

396.9

</td>
<td valign="top">

4.98

</td>
<td valign="top">

24

</td>
</tr>
<tr>
<td valign="top">

0.02731

</td>
<td valign="top">

0

</td>
<td valign="top">

7.07

</td>
<td valign="top">

0

</td>
<td valign="top">

0.469

</td>
<td valign="top">

6.421

</td>
<td valign="top">

78.9

</td>
<td valign="top">

4.9671

</td>
<td valign="top">

2

</td>
<td valign="top">

242

</td>
<td valign="top">

17.8

</td>
<td valign="top">

396.9

</td>
<td valign="top">

9.14

</td>
<td valign="top">

21.6

</td>
</tr>
</table>

This example graph can be used with any dataset that follows the above structure.

```
8. # Training a model using all columns to predict the last one.
9. cols <- colnames(df_train)
10. lm.fit <- lm(as.formula(paste(tail(cols, 1), '~.')),data=df_train)
```



### Model

The object model is converted to blob type and is output by the operator.

```
22. # Produce a blob model from your training dataset.
23. conn <- rawConnection(raw(0), "w")
24. saveRDS(cm.fit, conn)
25. modelBlob <- rawConnectionValue(conn)

```



### Metrics

The second output is a message type with the accuracy of the model. To compute it, 20% of the data is used to evaluation.

```
21. # Produce and save metrics in a JSON format.
22. json <- toJSON(data.frame(
23.     'RMSE'=toString(sqrt(mean(lm.fit$residuals^2)))
24. ))
```

