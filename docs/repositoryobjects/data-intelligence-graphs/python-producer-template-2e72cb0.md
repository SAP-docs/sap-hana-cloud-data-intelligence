<!-- loio2e72cb0e27b24068a830938d42804c94 -->

# Python Producer Template

The Python Producer template provides a basic structure to process data or train models using the Python language.



It consists of four steps, in which it:

1.  Reads file from data storage;

2.  Executes code in Python language to produce a new artifact and metrics;

3.  Saves artifact binary and metrics in the ML Scenario;

4.  Successfully completes the graph execution.




<a name="loio2e72cb0e27b24068a830938d42804c94__section_blf_vf5_1lb"/>

## Prerequisites

-   A file stored in one of the storage services available \(check Read File operator for more details\).

-   Adjusted Python code in Python3 operator to consume the content from Read File and to process the input data.




<a name="loio2e72cb0e27b24068a830938d42804c94__section_vly_wf5_1lb"/>

## Configure and Run

1.  In your ML Scenario, choose the Pipelines tab;

2.  Choose Create to create a new pipeline;

3.  Write a new name for your pipeline and select the Python Producer template from the drop-down list;

4.  Choose Create;

5.  Select your pipeline from the list and press Execute;

6.  Optional: write an execution description;

7.  On the Previous Configurations screen, select the Step 4 button to go to next configuration step;

8.  In Pipeline Parameters, write a new name for your model in NewArtifactName field and the file path in inputFilePath;

9.  Choose Save to execute the graph.




<a name="loio2e72cb0e27b24068a830938d42804c94__section_zf1_zjx_2lb"/>

## Python 3 Operator



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

Input



</td>
<td valign="top">

string



</td>
<td valign="top">

A string type with the file content provided by the Read File operator.



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

A key-value pair dictionary containing the metrics and their respective values.



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

The generated object in binary format.



</td>
</tr>
</table>



### Script

The code example has two main sections:

-   Metrics producer: create a dictionary with one or more metrics;

-   Model producer: you can use any Python package available in your docker image to process data or to train a model and save it as a binary object in the ML Scenario.


