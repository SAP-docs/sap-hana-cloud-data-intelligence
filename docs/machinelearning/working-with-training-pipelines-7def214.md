<!-- loio7def2149758741d59c28436d8ab21c3d -->

# Working with Training Pipelines

Using the SDK, you can create training jobs, including multi-file jobs, from within JupyterLab. To do so, you use the Training model to create a training pipeline.



<a name="loio7def2149758741d59c28436d8ab21c3d__section_lh4_frx_hjb"/>

## Creating a Training Pipeline Without an Input Artifact

You can create and execute a simple training pipeline based on the following code. A script file is generated and passed to the training operator to be executed. The script creates a model output artifact, which is available in the scenario within SAP Data Intelligence.

> ### Sample Code:  
> ```py
> from tempfile import NamedTemporaryFile
> from sapdi.training import Training
> 
> scriptContent = """
> from sapdi.artifact.artifact import Artifact, ArtifactKind, ArtifactFileType
> output_artifact = Artifact.create(
> artifact_alias='model',
> file_type=ArtifactFileType.FILE,
> file_name='model.xml',
> artifact_kind=ArtifactKind.MODEL,
> )"""
> 
> scriptFile = NamedTemporaryFile(mode='w+t')
> scriptFile.write(scriptContent)
> scriptFile.seek(0)
> 
> training = Training(script=scriptFile.name)
> handle = training.run()
> handle.wait_for_completion()
> ```



<a name="loio7def2149758741d59c28436d8ab21c3d__section_pfw_frx_hjb"/>

## Creating a Training Pipeline with an Input Artifact

You can create and execute a simple training pipeline based on the following code. In this case, an artifact is passed to the training operator and can be used inside the training script.

> ### Sample Code:  
> ```py
> from tempfile import NamedTemporaryFile
> from sapdi.training import Training
> import sapdi
> from sapdi.artifact.artifact import Artifact, ArtifactKind
> 
> created_artifact = sapdi.create_artifact(artifact_name='ArtifactName', artifact_kind=ArtifactKind.DATASET)
> created_full_artifact = sapdi.get_artifact(artifact_id=created_artifact.artifact_id)
> 
> file_handler = created_full_artifact.add_file(file_name='dataset.csv')
> file_handler.write('This is content')
> 
> scriptContent = """
> from sapdi.artifact.artifact import Artifact, ArtifactKind, ArtifactFileType
> import os
> 
> print(os.environ)
> output_artifact = Artifact.create(
> artifact_alias='model',
> file_type=ArtifactFileType.FILE,
> file_name='model.xml',
> artifact_kind=ArtifactKind.MODEL,
> )"""
> 
> scriptFile = NamedTemporaryFile(mode='w+t')
> scriptFile.write(scriptContent)
> scriptFile.seek(0)
> 
> training = Training(
>     input_artifacts={"dataset": created_full_artifact},
>     script=scriptFile.name,
> )
> handle = training.run()
> handle.wait_for_completion()
> ```



<a name="loio7def2149758741d59c28436d8ab21c3d__section_v4w_frx_hjb"/>

## Creating a Training Pipeline and Uploading a Script Folder

You can define a folder that is used inside the training script. The argument `scripts_folder` defines the path to the folder. The argument `script` defines the path to the file that is to be executed by the training script.

> ### Sample Code:  
> ```py
> 
> import os
> os.makedirs('scripts', exist_ok=True)
> with open('scripts/script.py', 'w+') as script:
>     script.write(scriptContent)
>     
> training = Training(scripts_folder='scripts', script='scripts/script.py')
> handle = training.run()
> handle.wait_for_completion()
> ```



<a name="loio7def2149758741d59c28436d8ab21c3d__section_my4_jk1_xlb"/>

## Creating a Training Pipeline from a Notebook

You can create a training script in a Jupyter notebook and submit it to a training pipline from a second notebook. For example, you create a script inside `notebook1.ipynb`:

```py

from sapdi.artifact.artifact import Artifact, ArtifactKind, ArtifactFileType
Artifact.create(
  artifact_alias='model',
  file_type=ArtifactFileType.FILE,
  file_name='model.xml',
  artifact_kind=ArtifactKind.MODEL
)
```

In a second notebook, you then submit the script to a training pipeline:

```py
from sapdi.training import Training
training = Training(script="notebook1.ipynb", scripts_folder=".")
handle = training.run()
handle.wait_for_completion()
```

