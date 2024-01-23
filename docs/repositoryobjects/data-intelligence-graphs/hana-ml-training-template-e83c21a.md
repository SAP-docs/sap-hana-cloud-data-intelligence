<!-- loioe83c21a4fe844841b57e06db7ec40dd1 -->

# HANA ML Training Template

The HANA ML Training template provides an example of a pipeline that uses the HANA PAL functionality to create a pipeline and store it in the data lake.



<a name="loioe83c21a4fe844841b57e06db7ec40dd1__section_r51_c15_1lb"/>

## Configure and Run

This graph is intended to be used from the Machine Learning Scenario Manager \(MLSM\) app.

Follow the steps below to run the template:

The request to the endpoint should look like the following:

1.  Open MLSM from the SAP DI Launchpad

2.  Create a scenario

3.  Create a pipeline and choose the HANA ML Inference template

4.  DI will open the Modeler app with the template

    Select the HANA ML Training operator and configure the following settings \(for details, check the operator documentation\):

    1.  Connection

    2.  Training Dataset

    3.  Training Features

    4.  Task

    5.  Algorithm

    6.  Test Dataset

    7.  Hyperparameters \(optional\)

    8.  Key Column

    9.  Target Column

    10. Fit Parameters \(optional\)


5.  Save the graph

6.  Go back to MLSM and run the pipeline

7.  When the wizard prompts for an artifact name, enter the name of the model to be created.


