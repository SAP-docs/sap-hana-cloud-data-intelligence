<!-- loio6e0e7e8173f748acab7cd2bcd71b7154 -->

# R Consumer - Exposing a trained ML model via API Example

This graph loads a trained ML model and exposes it via an API endpoint.



## Prerequisites

A trained model from your ML scenario to do inferences. If you don't have any ML models, please check the graph example R producer regression example or R producer classification example to train and create an ML model.



<a name="loio6e0e7e8173f748acab7cd2bcd71b7154__section_cvt_jdy_2lb"/>

## Configure and Run the Graph

1.  In your ML scenario, go to the *Pipelines* tab;

2.  Choose *Create* to create a new pipeline;

3.  Input a new name for your pipeline and select the *R Consumer Example Template* from the drop-down list;

4.  Choose *Create*;

5.  Find your pipeline on the list and select the *Deploy* button;

6.  Optional: write a deployment description;

7.  On the *Previous Configurations* screen, choose the*Step 4* button to go to next configuration step;

8.  On *Pipeline Parameters*, select your artifact model from the drop-down list and choose *Save*;

9.  When you get to *Deployment* screen, check if the status is *Running* and copy the Deployment URL.


Now, your API endpoint is available and you can use a client tool \(like Postman\) to use your ML model.



<a name="loio6e0e7e8173f748acab7cd2bcd71b7154__section_yg5_5fy_2lb"/>

## Postman Configuration



### Authorization Tab

-   Type: Basic Auth;

-   Username: <tenant\>\\<user\>;

-   Password: <your pass\>.




### Headers Tab

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



### Body Tab

A JSON with your data.

For example:

```
{
 "X0": [0.10, 0.20],
 "X1": [10.0, 20.0],
 "X2": [1, 0]
}
```



### Request

-   Type: `POST`

-   URL: `<URL deployment>/v1/inference/`

    -   'URL deployment' is the URL you copied from step 5 in the **Configure and Run the Graph** section.

    -   `/v1/inference/` is the path defined in the `swaggerSpec` field in the OpenAPI Servlow operator.



