<!-- loiodef1b2cba0b04414a8c5876beb779543 -->

# HANA ML Inference on API Requests

This is a template graph for the `HANA ML Inference` operator. The template is provided as an example of a pipeline to expose a previously trained model as a REST endpoint.



<a name="loiodef1b2cba0b04414a8c5876beb779543__section_r51_c15_1lb"/>

## Configure and Run

This graph is intended to be used from the Machine Learning Scenario Manager \(MLSM\) app.

Follow the steps below to run the template:

1.  Open MLSM from the SAP DI Launchpad

2.  Create a scenario

3.  Create a pipeline and choose the *HANA ML Inference* template. DI will open the Modeler app with the template

4.  Select the *HANA ML Inference* operator and configure the following settings \(for details, check the operator documentation\):

    1.  Connection

    2.  Key Column
    3.  Data Source = `Input Data Port`

5.  Save the graph

6.  Go back to MLSM and *deploy* the pipeline

7.  When the wizard prompts for the model to be used, select a previously trained one for the current scenario.

    The request to the endpoint should look like the following:

    ```
    curl --location --request POST 'https://<host>/app/pipeline-modeler/openapi/service/<deploy id>/v1/inference' \
    --header 'Content-Type: application/json' \
    --header 'If-Match: *' \
    --header 'X-Requested-With: Fetch' \
    --header 'Authorization: Basic #####' \
    --data-raw '{
            "ID": [1,2,3,...],
            "Column1": ["val1","val2","val3"...],
            "Column2": [10,20,30,...]
    }'
    ```


