<!-- loiod854956b5ac543b99fecfe392112dea0 -->

# HANA ML Inference on Dataset

This is a template graph for the `HANA ML Inference` operator with the option to use a dataset for inference. The template is provided as an example of a pipeline to expose a previously trained model and make inference on a provided dataset.



> ### Note:  
> The [Wiretap](../data-intelligence-operators/wiretap-2a0c233.md) operator can be replaced by any other operator the user may choose to handle the inference results.



<a name="loiod854956b5ac543b99fecfe392112dea0__section_srj_kqm_rnb"/>

## Configure and Run

This graph is intended to be used from the Machine Learning Scenario Manager \(MLSM\) app.

Follow the steps below to run the template:

1.  Open MLSM from the SAP DI Launchpad.

2.  Create a scenario.

3.  Create a pipeline and choose the *HANA ML Inference on Dataset* template. DI will open the Modeler app with the template.

4.  Select the *HANA ML Inference* operator and configure the following settings \(for details, check the operator documentation\):

    -   Connection

    -   Key Column
    -   Inference Dataset

5.  Save the graph.

6.  Go back to MLSM and *execute* the pipeline.

7.  When the wizard prompts for the model to be used, select a previously trained one for the current scenario.


