<!-- loio12f7abac63844d4293a339a8effb3521 -->

# Python SDK

The SAP Data Intelligence Python SDK is a high-level Python SDK that you can run in a Jupyter notebook as well as in a Pipeline operator \(in particular, the Training operator\).

The SDK provides convenient, programmatic access to SAP Data Intelligence functionality. For example, it helps you to perform the following:

-   Access ML scenarios and their versions, and also retrieve and update metadata
-   Create configurations, and start executions and deployments
-   Create and update pipelines and bind them to ML scenarios
-   Access artifacts from training containers
-   Report metrics through the ML Tracking SDK



## Importing the SDK

To get started with the SDK, import the `sapdi` module using the following command.

```py
import sapdi
```

-   **[About the Context](about-the-context-7b0bbf6.md "When working with an ML scenario, the context is already established as we are working
		within it. To retrieve the attributes of an ML scenario, simply access them as properties of
		the scenario object:")**  
When working with an ML scenario, the context is already established as we are working within it. To retrieve the attributes of an ML scenario, simply access them as properties of the scenario object:
-   **[Working with Pipelines](working-with-pipelines-62704e6.md "")**  

-   **[Versioning an ML Scenario](versioning-an-ml-scenario-e272d60.md "You can create a new version of your ML scenario or get the current version of the
		workspace.")**  
You can create a new version of your ML scenario or get the current version of the workspace.
-   **[Executing or Deploying Pipelines](executing-or-deploying-pipelines-6fb5e15.md "")**  

-   **[Working with Training Pipelines](working-with-training-pipelines-7def214.md "Using the SDK, you can create training jobs, including multi-file jobs, from within
		JupyterLab. To do so, you use the Training model to create a training pipeline.")**  
Using the SDK, you can create training jobs, including multi-file jobs, from within JupyterLab. To do so, you use the Training model to create a training pipeline.
-   **[Accessing Artifacts](accessing-artifacts-106e1c0.md "You can access artifacts from within JupyterLab or a pipeline using the methods from the
			Artifact class. The content of the artifacts is stored in the data
		lake.")**  
You can access artifacts from within JupyterLab or a pipeline using the methods from the `Artifact` class. The content of the artifacts is stored in the data lake.

