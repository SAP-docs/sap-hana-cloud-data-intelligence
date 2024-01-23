<!-- loio939fabf09e9e4556835a5ded329b988e -->

# ML Multi-Model Inference

The ML Multi-Model Inference template provides an example of an inference pipeline using the Model Serving operator to deploy multiple ML models and serve inference requests via an HTTP/REST endpoint. In particular, the graph shows how an HTTP inference request can be preprocessed by a Python operator to send a message to the Model Serving operator for the relevant model.



The Python *Preprocessor Operator* receives a message from the *OpenAPI Servlow* operator when an HTTP request is invoked and the pipeline is deployed. It does the following:

1.  Constructs the message attributes `mso.model_name` and `mso.method` with the values based on the received HTTP request URI and method as follows:


    <table>
    <tr>
    <td valign="top">
    
    `mso.method`
    
    </td>
    <td valign="top">
    
    If the HTTP request method is GET, the `mso.method` attribute value is set as `info`, which returns a list of the deployed models.

    If the HTTP request method is POST, the `mso.method` attribute value is set as `predict` to call the predict method on the model server for the given model name.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `mso.model_name`
    
    </td>
    <td valign="top">
    
    `mso.model_name` \(for which inference to be made\) is set as the value parsed from the HTTP request URI path parameter. For example, <code><i class="varname">&lt;OpenAPI Servlow URL&gt;</i>/v1/models/<i class="varname">&lt;model_name&gt;</i></code> where *<model\_name\>* is one of the model names that was configured in Models configuration. If a single model is deployed, the model name does not have to be passed in the URL path parameter.
    
    </td>
    </tr>
    </table>
    
    Based on the values of `mso.method` and `mso.model_name`, the following methods are called and return a response to the *OpenAPI Servlow* operator:

    -   `info` lists the models that are deployed on this model server.
    -   `predict` is an inference method for the given model name.

2.  Calls the *Model Serving Operator*. Based on the values `mso.method` and `mso.model_name`, the following methods are called and return a response to the *OpenAPI Servlow* operator as response.

    -   Method to list the models that are deployed on this model server.

        `predict` to call the predict method for the given model name on the model server.





<a name="loio939fabf09e9e4556835a5ded329b988e__section_scd_psb_vmb"/>

## Configure and Run the Graph

This graph is intended to be used from the *ML Scenario Manager* app and must be modified as follows in the *Modeler* app before it is deployed.

1.  Open *ML Scenario Manager* app from the Fiori launchpad.

2.  Select an existing ML scenario or create a new one as required.

3.  \(Skip this step if you already have a trained model.\) Choose the *Models* tab and register each of the models that you want to deploy.

4.  On the *Pipelines* tab, create a new pipeline:

    1.  Click *Create*.

    2.  Enter a name for your pipeline and select the *ML Multi-Model Inference* template from the dropdown list.

    3.  Click *Create*.


5.  Click the created pipeline to open the Modeler. The graph should be modified to add the models configuration before this pipeline is deployed.

6.  Modify the pipeline in the Modeler to fit your model deployment case. This mainly involves configuring the models as described at [Configure the Models List](ml-multi-model-inference-939fabf.md#loio939fabf09e9e4556835a5ded329b988e__section_n35_qtb_vmb).

    > ### Note:  
    > Use the `Models` configuration to deploy one or more models. If you specify both `artifactId` and `Models`, the graph will not run.

7.  After you have made the required changes, save the graph.

8.  Return to *ML Scenario Manager*, select your pipeline from the list, and click *Deploy*.

9.  Provide pipeline parameters such as `modelRuntimeId`, select the models from the dropdown, and save.

10. Monitor the pipeline status from the *Wiretap* operator in the Modeler. The deployment is ready for inference when it says ***Model is deployed and ready for inference***.

11. Copy the deployment URL from *ML Scenario Manager*.

    This is the URL to call the *OpenAPI Servlow* operator. It will receive the HTTP request and forward the request to the *Preprocessor Operator* in the template.

    The preprocessor constructs `mso.model_name` and `mso.method` message attributes and sends them to the *Model Serving Operator* to inference or list the models deployed based on the message attribute values that are sent.




<a name="loio939fabf09e9e4556835a5ded329b988e__section_n35_qtb_vmb"/>

## Configure the Models List

The models list is a list of models that are to be served. Each item in the list represents a model and contains two fields: *Name* and *ID*:

-   *Name* – The value of this field is used as the model name during deployment.

    This is an optional field. If it is empty, the ID \(`artifactId`\) is used as the model name.

    The name must be unique in the Models configuration. If a name is duplicated, the graph will become dead. You can use alphanumeric characters, hyphens, and underscores for the name. It cannot exceed 64 characters.

-   *ID* – This field receives the `artifactId` value of a model when the pipeline is deployed.

    It should be configured as <code>${ARTIFACT:MODEL:<i class="varname">&lt;modelname&gt;</i>}</code> so that it can be used in *ML Scenario Manager* to select from the registered models. `modelname` should be configured as a registered model name in *ML Scenario Manager* so that a model with that `modelname` is listed in the dropdown when the pipeline is deployed.




<a name="loio939fabf09e9e4556835a5ded329b988e__section_c41_5tb_vmb"/>

## Inference and List Models

Once the pipeline has been deployed, the model server is ready to serve the inference request. The model server can also be queried to list the deployed models.



### List Deployed Models

To list the models deployed:

-   End point: <code><i class="varname">&lt;Deployment URL from ML Scenario Manager Deployment&gt;</i>/v1/models</code>
-   HTTP Method: GET
-   Headers

    Header Key : Authorization

    Header Value : Basic *<Base64 Decoded value of "tenant/username" as "user name" and password\>*




### Inference

-   End point: <code><i class="varname">&lt;Deployment URL from ML Scenario Manager Deployment&gt;</i>/v1/models/{{model_name}}</code>

    `model_name` is the name of a model specified in the Models configuration. Alternatively, choose one from the list endpoint.

-   HTTP Method: POST

-   Payload Body: Inference data accepted by the model in JSON format

-   Headers:


    <table>
    <tr>
    <th valign="top">

    Header Key
    
    </th>
    <th valign="top">

    Header Value
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Authorization
    
    </td>
    <td valign="top">
    
    Basic <Base64 Encoded value of “tenant/username” as “user name” and password\>
    
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
    <tr>
    <td valign="top">
    
    X-Requested-With
    
    </td>
    <td valign="top">
    
    Fetch
    
    </td>
    </tr>
    </table>
    

