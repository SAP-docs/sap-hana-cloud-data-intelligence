<!-- loio969d99da4f6c4c5693c1ec954784f12a -->

# ML Batch Inference

The ML Batch Inference Example template uses file operators and the Model Serving operator to deploy an ML model and run batch inference for a given set of images. In particular, the graph shows how you can use a Python operator to prepare the input payload for TensorFlow Inception models by preprocessing the input image to base64-encoded JSON and sending it to the Model Serving operator for inference.



The sample *Inception Pre-processor* receives a `message.file` \(`JPG` files\) from the *Read File* operator once the pipeline is deployed. It then converts the file into base64-encoded JSON payload \(see below\) and sends it to the *Model Serving* operator.

```json
{
 "signature_name": "predict_images",
 "inputs": {
 "images": [
 {
 "b64": "<<<base64 encoded image here>>>"
 }
 ]
 }
}
```



<a name="loio969d99da4f6c4c5693c1ec954784f12a__section_w3t_52c_vmb"/>

## Before You Start

This example pipeline is a generic template that can be modified to handle any ML model and inference data. However, to run the example as is, you need `JPG` images for inference and a TensorFlow Inception model. Upload your data to `DI_DATA_LAKE` or a preferred Object Store Service such as S3. Then register the connection in *Connection Manager*. This graph also assumes a model has been trained and registered in *ML Scenario Manager*.



<a name="loio969d99da4f6c4c5693c1ec954784f12a__section_z5f_1fc_vmb"/>

## Configure and Run the Graph

This graph is intended to be originated \(or created\) as an ML Batch Inference pipeline from the *ML Scenario Manager* application.

Follow the steps below to use the template:



1.  Open *ML Scenario Manager* app from the Fiori launchpad.

2.  Select an existing ML scenario or create a new one as required.

3.  \(Skip this step if you already have a trained model.\) Choose the *Models* tab and register each of the models that you want to deploy.

4.  On the *Pipelines* tab, create a new pipeline:

    1.  Click *Create*.

    2.  Enter a name for your pipeline and select the *ML Batch Inference Example* template from the dropdown list.

    3.  Click *Create*.

        The *Modeler* application will open in a new tab in your browser. If it doesn’t, click the pipeline name to open it.


5.  Modify the pipeline in the *Modeler* app.

    -   *Model Serving Operator* has been configured to deploy a single model using the substitution parameter `${ARTIFACT:MODEL}` in Models configuration. If you want to deploy multiple models, add more items to the list. The operator is also configured to accept the model runtime via `${ModelRuntimeId}`.

    -   The *List File* and *Write File* operators are configured with substitute parameter `${InputFilePath}` to accept the directory path containing `JPG` files from the `DI_DATA_LAKE` connection. Change the *List File* and *Write File* operators accordingly if you want to use another connection.

    -   The *Inception Preprocessor* operator is a simple Python3 operator with preprocessing code to create a prediction JSON request for a TensorFlow Inception model. This is sample code that you must modify for productive use.


6.  After you have made the required changes, save the graph.

7.  Return to *ML Scenario Manager*, select your pipeline from the list, and click *Execute*.

8.  Enter the pipeline parameters when prompted.

    -   Select a model from the dropdown list.
    -   Set the `ModelRuntimeId` as `mlserving-1.1` or `tf-1.15`.
    -   Set the `InputFilePath` as the actual path of a directory containing the images data. For example, `/shared/my_sample_data/images`.
    -   Click *Save* to trigger the pipeline.

9.  Go back to the *Modeler* app to monitor the pipeline status. You can open the UI of the *Wiretap* operator for the running pipeline to follow the log messages.

10. Once the pipeline is completed, inference outputs will be written to `${InputFilePath}/results.txt`. For example, if your `${InputFilePath}` is set to `/shared/my_sample_data/images`, prediction outputs from the model will be written to `/shared/my_sample_data/images/results.txt`. You can download this file or view its contents in the *Metadata Explorer* app.


