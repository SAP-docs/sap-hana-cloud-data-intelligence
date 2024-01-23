<!-- loio749755fa7abb4c1cb52fff37aafd1c2f -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Executing and Deploying Pipelines

The *Pipeline* tab contains pipelines that have been created in ML Scenario Manager. Each pipeline can be executed or deployed depending on its type. Training pipelines can be executed, and inference pipelines can be deployed. Executed or deployed pipelines are shown on the corresponding tabs.



<a name="loio749755fa7abb4c1cb52fff37aafd1c2f__prereq_tk1_wxm_b3b"/>

## Prerequisites

You have saved any changes you have made to your scenario.



<a name="loio749755fa7abb4c1cb52fff37aafd1c2f__steps_gbm_5gc_fhb"/>

## Procedure

1.  On the scenario details page, click the *Pipelines* tab and select the radio button for the pipeline that you want to execute or deploy.

2.  Execute or deploy the pipeline by clicking the corresponding icon.

    -   :fast_forward: executes a training pipeline.
    -   <span class="SAP-icons"></span> deploys an inference pipeline.

3.  Enter a description for your configuration.

4.  **Optional:** If you want to use a previous configuration to populate the pipeline parameters, select it from the list.

5.  Enter your pipeline parameters.




<a name="loio749755fa7abb4c1cb52fff37aafd1c2f__result_zsl_qhc_fhb"/>

## Results

The results are shown on the *Executions* and *Deployment* tabs. Executing a training pipeline also generates a model.

**Related Information**  


[Adding a Pipeline](adding-a-pipeline-91ec15e.md "Pipelines represent a step-by-step process to execute a specific activity, such as data extraction, data transformation, training, or model serving. ML Scenario Manager provides templates that you can use as a starting point to create your own pipelines.")

