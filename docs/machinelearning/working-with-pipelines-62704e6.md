<!-- loio62704e6231f44ad095e641b28cd0c4e6 -->

# Working with Pipelines



## Context

ML scenarios are containers for pipelines. To set up a pipeline, follow these steps:



## Procedure

1.  Add new pipelines to your ML scenario:

    ```
    pipeline = sapdi.create_pipeline("mypipeline", description="This is my training pipeline", from_template="com.sap.dsp.templates.tensorflow_training_template")
    ```

2.  Define graphs for the pipelines by creating operators, such as a Training and Terminal operator:

    ```
    script = """
    import sapdi
    
    print("Hello world")
    out_artifact = sapdi.create_artifact("model", file_type=sapdi.artifact.ArtifactFileType.FOLDER, description="Best model ever", artifact_name="Model")
    """
    
    train = sapdi.pipeline.operators.com.sap.ml.training(script = script, image='com.sap.mlf/tyom-tf-1.12.0-py36-cpu')
    
    train.outputs.create_port("model", "message.artifact")
     
    term = sapdi.pipeline.operators.com.sap.dh.terminator()
    ```

3.  Connect the operators:

    ```
    term.inputs.stop = train.outputs.model
    
    ```

4.  Add the operators to a Graph object and assign them to the pipeline in your ML scenario:

    ```
    pipeline.graph = sapdi.pipeline.Graph(operators = term)
    ```


