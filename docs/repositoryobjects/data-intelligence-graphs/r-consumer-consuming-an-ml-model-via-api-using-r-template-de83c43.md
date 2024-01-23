<!-- loiode83c43b60d24d1990db5874336baf9d -->

# R Consumer - Consuming an ML Model via API using R Template

This template provides a basic structure to consume a trained ML model and expose it via API endpoint. The RClient - Inference operator loads a model binary from Artifact Producer and receives input data from the OpenAPI Servlow operator.



## Prerequisites

-   A model binary stored in ML Scenario \(you can create one using the R Producer template\).

-   Adjust the R code in RClient - Inference operator to perform inference using your model.




<a name="loiode83c43b60d24d1990db5874336baf9d__section_cbd_5g5_1lb"/>

## Configure and Run

1.  In your ML scenario, go to the Pipelines tab;

2.  Choose Create to create a new pipeline;

3.  Input a new name for your pipeline and select the R Consumer template from the drop-down list;

4.  Choose Create;

5.  Select your pipeline from the list and select the Deploy button;

6.  Optional: write a deployment description;

7.  On the Previous Configurations screen, choose the Step 4 button to go to next configuration step;

8.  On Pipeline Parameters, select your artifact model from the drop-down list and choose Save;

9.  When you get to Deployment screen, check if the status is "Running" and copy the Deployment URL.


Now, your API endpoint is available and you can use a client tool \(like Postman\) to use your ML model.



<a name="loiode83c43b60d24d1990db5874336baf9d__section_ojq_1h5_1lb"/>

## RClient Inference operator



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

model

</td>
<td valign="top">

blob

</td>
<td valign="top">

Model in binary format loaded using the Artifact Consumer operator.

</td>
</tr>
<tr>
<td valign="top">

input

</td>
<td valign="top">

message

</td>
<td valign="top">

A message type received from API endpoint containing the input data.

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

response

</td>
<td valign="top">

message

</td>
<td valign="top">

A message type to be returned as API response containing the result of your model inference.

</td>
</tr>
</table>



### Script

The code example loads the model and checks if the input data is a valid JSON format. In order to process the incoming data, you need to replace the comment "apply model & generate results" by the predict function of your model and create a response using these results.



### Postman Configuration

-   Authorization Tab

    Type: Basic Auth

    Username: <tenant\>\\<user\>

    Password: <your pass\>


-   Headers tab

    ****


    <table>
    <tr>
    <th valign="top">

    Key
    
    </th>
    <th valign="top">

    Value
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    If-Match
    
    </td>
    <td valign="top">
    
    \*
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    x-requested-with
    
    </td>
    <td valign="top">
    
    Fetch
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Content-Type
    
    </td>
    <td valign="top">
    
    application/json
    
    </td>
    </tr>
    </table>
    

-   Body Tab

    A JSON with your data.

    For example:

    ```
    {
     "X0": [0.10, 0.20],
     "X1": [10.0, 20.0],
     "X2": [1, 0]
    }
    ```


-   Request

    Type: POST

    URL: <URL deployment\>/v1/uploadjson/

    -   'URL deployment' is the URL you copied from step 5 in the \`Configure and Run the Graph section.

    -   '/v1/uploadjson/' is the path defined in the swaggerSpec field in the OpenAPI Servlow operator.



