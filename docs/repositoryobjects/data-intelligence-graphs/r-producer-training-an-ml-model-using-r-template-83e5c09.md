<!-- loio83e5c09ba1e7466f89ff289916112f0c -->

# R Producer - Training an ML Model Using R Template

This template provides a basic structure to train an ML model using R language.



It consists of four steps:

1.  Reads file from data storage;

2.  Executes code in R to produce a new artifact and metrics;

3.  Saves artifact binary and metrics in the ML Scenario;

4.  Completes the graph execution.




<a name="loio83e5c09ba1e7466f89ff289916112f0c__section_blf_vf5_1lb"/>

## Prerequisites

-   A file stored in one of the storage services available \(check Read File operator for more details\).

-   Adjusted R code in RClient - Training operator to consume the content from Read File and to process the input data.




<a name="loio83e5c09ba1e7466f89ff289916112f0c__section_vly_wf5_1lb"/>

## Configure and Run

1.  In your ML Scenario, choose the *Pipelines* tab;

2.  Choose *Create* to create a new pipeline;

3.  Write a new name for your pipeline and select the `R Producer` template from the drop-down list;

4.  Choose *Create*;

5.  Select your pipeline from the list and press *Execute*;

6.  Optional: write an execution description;

7.  On the *Previous Configurations* screen, select the *Step 4* button to go to next configuration step;

8.  In Pipeline Parameters, write a new name for your model in `NewArtifactName` field and the file path in `inputFilePath`;

9.  Choose *Save* to execute the graph.


Check out the [Python3 Operator](../data-intelligence-operators/python3-operator-0211803.md) documentation for further information.



<a name="loio83e5c09ba1e7466f89ff289916112f0c__section_syz_c3v_1lb"/>

## RClient Training Operator



### Input

****


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

message

</td>
<td valign="top">

message

</td>
<td valign="top">

A message type with all file information provided by the Read File operator.

</td>
</tr>
</table>



### Output

****


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

metrics

</td>
<td valign="top">

message

</td>
<td valign="top">

A key-value pair dictionary containing the metrics and their respective values

</td>
</tr>
<tr>
<td valign="top">

modelBlob

</td>
<td valign="top">

blob

</td>
<td valign="top">

The generated model in binary format.

</td>
</tr>
</table>



### Script

The code example has three main sections:

-   Model producer: you can use any R package available in your docker image to train a model and convert it to binary data;

-   Metrics producer: create a JSON with one or more metrics;

-   Outputs producer: list containing model binary and metrics.


