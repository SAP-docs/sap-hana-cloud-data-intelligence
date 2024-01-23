<!-- loio32fd2654d8554f0798a0046da53a3d59 -->

# Python Data Preprocessing Example

The Python Data Preprocessing Example template provides a sample graph that illustrates how to undertake data preprocessing with Python, register a dataset, and submit metrics in an ML scenario.



A file in CSV format is read by the Read File and will be delivered through the outFile output port. The data will be fed into the Python Operator through the ToString converter as string.

In the Python3 operator, metrics are created and the raw dataset is preprocessed.

The metrics are delivered to the Submit Metrics operator, which registers the metrics as part of the scenario.

The dataset is sent to the Artifact Producer operator, which will register the dataset with an artifact ID. In the Configuration, the following parameters are set with the default value:

-   Artifact Kind: `dataset`

-   Filename Suffix: `.csv`


When both the response of Submit Metrics and the Artifact Producer are delivered to the Operators Complete operator, a message will be sent to the Graph Terminator operator and the graph will complete.



<a name="loio32fd2654d8554f0798a0046da53a3d59__section_c4r_ysx_2lb"/>

## Prerequisites

A CSV file stored in vrep with columns separated by semicolon \(;\). In the example, the file is saved under `/files/vflow/blobs/com/sap/ml/sampleData/boston_housing_dataset.csv`.



<a name="loio32fd2654d8554f0798a0046da53a3d59__section_znd_dtx_2lb"/>

## Configure and Run the Graph

1.  In your ML scenario, choose the Pipelines tab;

2.  Choose Create to create a new pipeline;

3.  Write a new name for your pipeline and select the Python Data Preprocessing Example template from the drop-down list;

4.  Choose Create;

5.  Select your pipeline from the list and press the Execute;

6.  Optional: write an execution description;

7.  On the Previous Configurations screen, press Step 4 to go to next configuration step;

8.  In Pipeline Parameters, write a new name for your model in NewArtifactName field;

9.  Choose Save to execute the graph.




<a name="loio32fd2654d8554f0798a0046da53a3d59__section_sx4_mtx_2lb"/>

## Dataset

Here we are using the Boston Housing dataset as an example to do data preprocessing. It is assumed that the last column of the input dataset is the target column. A sample of the CSV file is shown below:


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

medv



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



<a name="loio32fd2654d8554f0798a0046da53a3d59__section_ikt_mtx_2lb"/>

## Basic Examples



### Remove feature with high correlation

```
ef remove_high_corr(data, unrelated_cols):
    df_o = data
    df_u = df_o.drop(columns=unrelated_cols)
    cor = df_u.corr()
    cor_cols = [j for i in range(len(df_u.columns)) for j in range(i+1, len(df_u.columns)) if cor.iloc[i, j] >= 0.9]    
    cols = [False if index in cor_cols else True for index in range(len(df_u.columns))]
    sel_cols = df_u.columns[cols]
    df_new = df_u[sel_cols]
    df_new[unrelated_cols] = df_o[unrelated_cols]
    return df_new
```

This method removes one of the two features that have high correlation with each other \(corr \>= 0.9\). In the example, the column **tax** is removed due to the high correlation with the column **rad**.

-   **Input**

    -   data: pandas DataFrame

    -   unrelated\_cols: string or list of string, columns that should be excluded for the correlation assessment such as target column


-   **Output**
    -   df\_new: new DataFrame with selected Columns





### Fill NaN cells

-   To replace the **NaN** value with **0**`0:df_final = df.fillna(0)`

-   To replace the **NaN** value with column **mean**: `df_final = df.fillna(df.mean())`




### Remove Outliers

```
def remove_outlier(data, unrelated_cols):
    df_o = data
    df_u = df_o.drop(columns=unrelated_cols)
    df_zscore = (df_u - df_u.mean())/df_u.std()
    df_new = df_o[(df_zscore<3).all(axis=1)]
    return df_new
```

This method removes the rows that contain data points more than 3 standard deviations away from the mean. In this example, 67 rows of data are removed.

-   **Input**

    -   data: pandas DataFrame

    -   unrelated\_cols: string or list of string, DataFrame column names that shouldn’t be assessed, for example the target column.


-   **Output**

    -   df\_new: new DataFrame with removed outliers.





### One Hot Encoding

```
def one_hot_encoding(data):
    return pd.get_dummies(data)
```

This method changes the encoding of columns that contain categorical data to numerical data.

-   **Input**

    -   data: pandas DataFrame


-   **Output**

    -   new pandas DataFrame with encoded numerical data.



