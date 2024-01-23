<!-- loio45a787e9f5974426bbb8b3096609b0b0 -->

# R Producer - Training a classification model using R Example

This graph consumes data from a CSV file stored in the Local File System \(vrep\) to train a classification model using the method recursive partitioning from the package rpart.



As an example, we use the Iris dataset to train a model able to classify iris flowers based on a given set of features.



<a name="loio45a787e9f5974426bbb8b3096609b0b0__section_n2m_5hy_2lb"/>

## Prerequisites

A CSV file stored in vrep with columns separated by semicolon \(';'\).



<a name="loio45a787e9f5974426bbb8b3096609b0b0__section_cvt_jdy_2lb"/>

## Configure and Run the Graph

1.  In your ML scenario, go to the *Pipelines* tab;

2.  Choose *Create* to create a new pipeline;

3.  Input a new name for your pipeline and select the *R Producer Classification Example* from the drop-down list;

4.  Choose *Create*;

5.  Find your pipeline on the list and select the *Deploy* button;

6.  Optional: write a deployment description;

7.  On the *Previous Configurations* screen, choose the*Step 4* button to go to next configuration step;

8.  On *Pipeline Parameters*, write a new name for your model in the `NewArtifactName` field; and choose *Save*;

9.  Execute your graph.



<a name="loio45a787e9f5974426bbb8b3096609b0b0__section_ksf_s3y_2lb"/>

## Training Operator



### Ports

-   Input

    -   Input: A message type with all file information provided by the read file operator.


-   Output

    -   metrics: Model artifact to be saved;

    -   modelBlob: Model metrics.





### Dataset

The following is a sample of the CSV file with the Iris dataset. It is assumed that the target values are provided in the last column.

****


<table>
<tr>
<th valign="top">

sepal\_length

</th>
<th valign="top">

sepal\_width

</th>
<th valign="top">

petal\_length

</th>
<th valign="top">

petal\_width

</th>
<th valign="top">

class

</th>
</tr>
<tr>
<td valign="top">

5.1

</td>
<td valign="top">

3.5

</td>
<td valign="top">

1.4

</td>
<td valign="top">

0.2

</td>
<td valign="top">

Iris-setosa

</td>
</tr>
<tr>
<td valign="top">

7.0

</td>
<td valign="top">

3.2

</td>
<td valign="top">

4.7

</td>
<td valign="top">

1.4

</td>
<td valign="top">

Iris-versicolor

</td>
</tr>
<tr>
<td valign="top">

7.2

</td>
<td valign="top">

6.1

</td>
<td valign="top">

6.1

</td>
<td valign="top">

2.5

</td>
<td valign="top">

Iris-virginica

</td>
</tr>
</table>

This example graph can be used with any dataset that follows the above structure.

```
14. # Training a model using all columns to predict the last one.
15. cols <- colnames(df_train)
16. cm.fit<-rpart(as.formula(paste(tail(cols, 1), '~.')),data=df_train)
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

