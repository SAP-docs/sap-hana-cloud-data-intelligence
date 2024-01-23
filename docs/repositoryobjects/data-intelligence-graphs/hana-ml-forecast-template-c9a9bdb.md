<!-- loioc9a9bdb3c5c44f7893248300ef3c7069 -->

# HANA ML Forecast Template

The HANA ML Forecast template provides an example of a pipeline to forecast data immediately without the need to persist a model.



<a name="loioc9a9bdb3c5c44f7893248300ef3c7069__section_r51_c15_1lb"/>

## Configure and Run

This graph is intended to be used from the *Machine Learning Scenario Manager* app.

Follow the steps below to run the template:

1.  Open *ML Scenario Manager* from the launchpad.

2.  Create a scenario.

3.  Create a pipeline and choose the *HANA ML Forecast* template.

    The *Modeler* app appears containing the template.

4.  Select the HANA ML Forecast operator and configure \(at least \) the following settings \(for details, check the operator documentation\):

    -   Connection
    -   Algorithm
    -   Key Column

5.  Save the graph.

6.  Go back to ML Scenario Manager and deploy the pipeline.


> ### Example:  
> The request that can be made to the operator could be as follows:
> 
> ```
> curl --location --request POST 'https://<host>/app/pipeline-modeler/openapi/service/<deploy id>/v2/inference' \
> --header 'Content-Type: application/json' \
> --header 'If-Match: *' \
> --header 'X-Requested-With: Fetch' \
> --header 'Authorization: Basic #####' \
> --data-raw '{
>       "data": {
>          "ID": [1,2,3,...],
>          "Y": [10,20,30,...]
>       }
>    }'
> ```

**Related Information**  


[HANA ML Forecast](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/083780c468204924b286b6d595466d20.html "The HANA ML Forecast operator connects to an SAP HANA database and leverages algorithms from SAP HANA Predictive Analytics Library (PAL) or SAP HANA Automated Predictive Library (APL) that do not require a model to be persisted. Instead, the model is generated on-the-fly based on the input data, and a series of results are then forecast automatically.") :arrow_upper_right:

