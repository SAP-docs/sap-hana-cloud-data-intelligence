<!-- loio91ec15ead2e84fad98438e899b99a154 -->

# Adding a Pipeline

Pipelines represent a step-by-step process to execute a specific activity, such as data extraction, data transformation, training, or model serving. *ML Scenario Manager* provides templates that you can use as a starting point to create your own pipelines.



## Procedure

1.  On the *Pipelines* tab scenario details page, click *Create*.

2.  In the *Create Pipeline* dialog box, enter a unique name and \(optionally\) a description.

    > ### Note:  
    > You can change the name and description of your pipeline at any time by selecting the pipeline from the scenario details screen and clicking *Edit*.

3.  Select one of the following templates to build a pipeline:


    <table>
    <tr>
    <th valign="top">

    Template
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Basic Training
    
    </td>
    <td valign="top">
    
    The Basic Training template provides a basic structure to use the Training operator to train TensorFlow models.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Blank
    
    </td>
    <td valign="top">
    
    The Blank template allows you to create your ML models from scratch.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    HANA ML Forecast
    
    </td>
    <td valign="top">
    
    The HANA ML Forecast template demonstrates a pipeline that performs data forecasting in real-time without the requirement to store a model persistently.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    HANA ML Inference
    
    </td>
    <td valign="top">
    
    The HANA ML Inference template showcases a pipeline that exposes a pre-trained model as a REST endpoint.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    HANA ML Training
    
    </td>
    <td valign="top">
    
    The HANA ML Training template demonstrates a pipeline that utilizes the HANA PAL \(Predictive Analytics Library\) functionality to create a pipeline for training machine learning models. The trained models are then stored in the data lake for further analysis and usage.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    ML Batch Inference Example
    
    </td>
    <td valign="top">
    
    The ML Batch Inference Example template is designed to showcase the usage of file operators and the Model Serving operator to deploy an ML model and perform batch inference on a specified set of images. The graph demonstrates the integration of a Python operator to preprocess the input images, converting them into base64-encoded JSON format, which is then sent to the Model Serving operator for inference using TensorFlow Inception models.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    ML Multi-Model Inference
    
    </td>
    <td valign="top">
    
    The ML Multi-Model Inference template provides an example of an inference pipeline using the Model Serving operator to deploy multiple ML models and serve inference requests via an HTTP/REST endpoint. In particular, the graph shows how an HTTP inference request can be preprocessed by a Python operator to send a message to the Model Serving operator for the relevant model.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Python Consumer
    
    </td>
    <td valign="top">
    
    The Python Consumer template provides a basic structure to consume a trained ML model and expose it via an API endpoint. The Python3 inference operator loads a model binary from the Artifact Producer and receives input data from the OpenAPI Servlow operator.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Python Data Preprocessing Example
    
    </td>
    <td valign="top">
    
    The Python Data Preprocessing Example template provides a sample graph that illustrates how to undertake data preprocessing with Python, register a dataset, and submit metrics in an ML scenario.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Python Producer
    
    </td>
    <td valign="top">
    
    The Python Producer template provides a basic structure to process data or train models using the Python language.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Pytorch Text Classification Example
    
    </td>
    <td valign="top">
    
    The Pytorch Text Classification Example template illustrates how to use the Training operator to train a supervised learning algorithm for classification using Pytorch, and submit metrics in an ML scenario.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    R Consumer
    
    </td>
    <td valign="top">
    
    The R Consumer template provides a basic structure to consume a trained ML model and expose it via API endpoint.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    R Consumer Example
    
    </td>
    <td valign="top">
    
    The R Consumer Example template loads a trained ML model and exposes it via an API endpoint.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    R Producer
    
    </td>
    <td valign="top">
    
    The R Producer template provides a basic structure to train an ML model using the R language.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    R Producer Classification Example
    
    </td>
    <td valign="top">
    
    The R Producer Classification Example template consumes data from a CSV file stored in the local file system \(vrep\) to train a classification model using the recursive partitioning method from the package rpart. As an example, we use the Iris dataset to train a model that can classify iris flowers based on a given set of features.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    R Producer Regression Example
    
    </td>
    <td valign="top">
    
    The R Producer Regression Example template consumes data from a CSV file stored in the local file system \(vrep\) to create a linear regression model using the “lm” function. In this example, we use the Boston Housing dataset to train a model that can predict the median value of owner-occupied homes in thousands of dollars.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    TensorFlow 2 and Scikit Structured Data Classification
    
    </td>
    <td valign="top">
    
    The TensorFlow 2 and Scikit Structured Data Classification template illustrates how to use the Training operator to train a structured data classification model with TensorFlow 2, and to submit metrics in an ML scenario. It uses a small dataset provided by the Cleveland Clinic Foundation for Heart Disease.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    TensorFlow MNIST Training Example
    
    </td>
    <td valign="top">
    
    The TensorFlow MNIST Training Example template illustrates how to use the Training operator to train an imageclassification model using the MNIST dataset with TensorFlow, and to submit metrics in an ML scenario.
    
    </td>
    </tr>
    </table>
    
    For more information about each of these templates, see [ML Scenario Manager Templates and Examples](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/ddd565eeb5ce4b9f844f839497e102c9.html "") :arrow_upper_right:.

4.  Click *Create* to create your pipeline.

    Your pipeline opens in the SAP Data Intelligence Modeler.


-   **[Executing and Deploying Pipelines](executing-and-deploying-pipelines-749755f.md "The Pipeline tab contains pipelines that have been created in ML
		Scenario Manager. Each pipeline can be executed or deployed depending on its type. Training
		pipelines can be executed, and inference pipelines can be deployed. Executed or deployed
		pipelines are shown on the corresponding tabs.")**  
The *Pipeline* tab contains pipelines that have been created in ML Scenario Manager. Each pipeline can be executed or deployed depending on its type. Training pipelines can be executed, and inference pipelines can be deployed. Executed or deployed pipelines are shown on the corresponding tabs.

**Related Information**  


[ML Scenario Manager Templates and Examples](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/ddd565eeb5ce4b9f844f839497e102c9.html "") :arrow_upper_right:

[Introduction to the SAP Data Intelligence Modeler](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/f003a9f0eea3439488202faeb5ef6d5f.html "The SAP Data Intelligence Modeler application is based on the Pipeline Engine, which uses a flow-based programming model to run graphs that process your data.") :arrow_upper_right:

