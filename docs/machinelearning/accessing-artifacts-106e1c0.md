<!-- loio106e1c0a2f2c4abb804e0de6ad909cda -->

# Accessing Artifacts

You can access artifacts from within JupyterLab or a pipeline using the methods from the `Artifact` class. The content of the artifacts is stored in the data lake.

The `Artifact` class contains all of the methods that you need to access an artifact:


<dl>
<dt><b>

add\_file

</b></dt>
<dd>

Adds a file to the artifact and returns a file handler to read or write it.



</dd><dt><b>

create

</b></dt>
<dd>

Creates or registers an artifact with basic information, and returns the artifact ID so that you can retrieve all of the metadata for the artifact. You can upload a folder or a file to the data lake when the artifact is created. This method can also be called directly from the `sapdi` module.



</dd><dt><b>

delete

</b></dt>
<dd>

Deletes an artifact based on its ID. Note that this method does **not** delete the content.



</dd><dt><b>

delete\_content

</b></dt>
<dd>

Deletes the artifact content in the artifact storage.



</dd><dt><b>

download

</b></dt>
<dd>

Downloads all of the artifact content or a specific file from the artifact.



</dd><dt><b>

get

</b></dt>
<dd>

Retrieves the artifact metadata. This method can also be called directly from the `sapdi` module.



</dd><dt><b>

list

</b></dt>
<dd>

Lists all of the artifacts that are currently registered with the scenario. This method can also be called directly from the `sapdi` module.



</dd><dt><b>

open\_file

</b></dt>
<dd>

Returns a file handler to read or write the remote files stored in the data lake.



</dd><dt><b>

upload

</b></dt>
<dd>

Uploads a file or folder to the artifact.



</dd><dt><b>

walk

</b></dt>
<dd>

Depth-first walk of the artifact.



</dd>
</dl>

The `FileHandler` class contains methods that you can use to read or write files:


<dl>
<dt><b>

get\_reader

</b></dt>
<dd>

Returns an object with an interface similar to the python `file` object. This method must be called within a `with` statement.



</dd><dt><b>

get\_writer

</b></dt>
<dd>

Returns an object with an interface similar to the python `file` object, which can be used to write the file incrementally. This method must be called within a `with` statement.



</dd><dt><b>

read

</b></dt>
<dd>

Reads the entire remote file in the data lake.



</dd><dt><b>

write

</b></dt>
<dd>

Writes data \(string, bytes, files\) to the remote data lake.



</dd>
</dl>

> ### Restriction:  
> Only files between 5 MB and 5 GB can be appended. `FilerHandler#write` will raise an exception if this condition is not met. Use `FileHandler#get_writer` instead.



<a name="loio106e1c0a2f2c4abb804e0de6ad909cda__section_pr3_1yw_hjb"/>

## Examples

The following sections show how you can use the methods above to access artifacts from JupyterLab or from within a pipeline. Before you begin, check that the `sapdi` module is available in your execution content.



### Create an Artifact

This example creates an empty artifact:

```py
import os
import sapdi
from sapdi.artifact.artifact import ArtifactKind, ArtifactFileType

artifact_simple = sapdi.create_artifact(
	artifact_kind=ArtifactKind.DATASET, 
	artifact_name='My Dataset', 
	description='My Description'
	)
artifact_simple.__dict__
```

Running this code returns the following:

> ### Output Code:  
> ```
> {'artifact_id': '6e1993e1-6c68-44ea-8808-2dc503c0adbc',
>  'artifact_alias': None,
>  'name': 'My Dataset',
>  'description': 'My Description',
>  'kind': <ArtifactKind.DATASET: 'dataset'>,
>  'file_type': <ArtifactFileType.FOLDER: 'folder'>,
>  '_access_mode': None,
>  '_metadata': {'uri': 'dh-dl://DI_DATA_LAKE/shared/ml/artifacts/notebooks/test.ipynb/548a2e0d-baa9-4a15-8df0-4bf9e80a0cc4'},
>  '_storage': <sapdi.internal.datalake.datalake_storage.DatalakeStorage at 0x7f8fa5248828>,
>  'datacollection_id': ''}
> ```

By default, an artifact of type “folder” is created and multiple files and directories can be added to it. An artifact of type “folder” can also be created explicitly:

```py
artifact_folder = sapdi.create_artifact(
    artifact_name='folder_artifact',
    artifact_kind=ArtifactKind.DATASET,
    description='folder artifact description',
    file_type=ArtifactFileType.FOLDER
)
```

An artifact of type “file” can also be created to represent a single file. No other additional file or directory can be put into this artifact once it has been created:

```py
artifact_folder = sapdi.create_artifact(
    artifact_name='file_artifact',
    artifact_kind=ArtifactKind.DATASET,
    description='file artifact description',
    file_type=ArtifactFileType.FILE,
    file_name='file_name.ext'
)
```

An artifact can also be created from an existing local folder:

```py
os.makedirs('upload', exist_ok=True)
with open('upload/upload.txt', 'w+') as upload:
    upload.write('abcdefghijklm')
    
artifact_with_content = sapdi.create_artifact(artifact_kind=ArtifactKind.DATASET, artifact_name='My Dataset', description='My Description', upload_content='upload')
artifact_with_content.open_file('upload.txt').read()
```



### Create an Artifact in a Python 3 Operator Script

You can use the SDK inside a Python 3 operator script as long as the operator is placed inside a group and the group is configured with the `sapdi` tag. If you don't need a specific version, you can leave the version dropdown blank.

The following example shows you how to create an artifact in a Python 3 operator script:

```py
import sapdi
from sapdi.artifact.artifact import ArtifactKind

# Create a folder artifact from a file
artifact = sapdi.create_artifact(
    artifact_name='folder_artifact',
    artifact_kind=ArtifactKind.DATASET
)
```



### List Artifacts

This example lists the artifacts that are registered in the current scenario.


<table>
<tr>
<th valign="top">

Using `sapdi`

</th>
<th valign="top">

Using the `Artifact` class

</th>
</tr>
<tr>
<td valign="top">

```py
import sapdi
scenario = sapdi.get_current_scenario()
artifacts = sapdi.list_artifacts(scenario=scenario)
```



</td>
<td valign="top">

```py
from sapdi.artifact.artifact import Artifact
scenario = sapdi.get_current_scenario()

artifacts = Artifact.list(scenario=scenario)
```



</td>
</tr>
</table>



### Delete an Artifact

This example deletes an artifact based on its ID.


<table>
<tr>
<th valign="top">

Using `sapdi`

</th>
<th valign="top">

Using the `Artifact` class

</th>
</tr>
<tr>
<td valign="top">

```py
import sapdi
artifact = sapdi.delete_artifact(artifact_id='xxxxx-yyyyy-zzzzz')
```



</td>
<td valign="top">

```py
from sapdi.artifact.artifact import Artifact
artifact = Artifact.delete(artifact_id='xxxxx-yyyyy-zzzzz')

```



</td>
</tr>
</table>



### Retrieve an Artifact

This example retrieves an artifact using its ID.


<table>
<tr>
<th valign="top">

Using `sapdi`

</th>
<th valign="top">

Using the `Artifact` class

</th>
</tr>
<tr>
<td valign="top">

```py
import sapdi

artifact = sapdi.get_artifact(artifact_id='xxxxx-yyyyy-zzzzz')
```



</td>
<td valign="top">

```py
from sapdi.artifact.artifact import Artifact

artifact = Artifact.get(artifact_id='xxxxx-yyyyy-zzzzz')
```



</td>
</tr>
</table>



### Read a File from an Artifact

This example reads the content of a file contained in an artifact. The content can be read in the following ways:

-   Inside a `with` statement if a deferred reading is needed using `get_reader`
-   Calling `read` if all of the content needs to be read at once

```py
from sapdi.artifact.artifact import Artifact

artifact = Artifact.get(artifact_id='xxxxx-yyyyy-zzzzz') 

file_handler = artifact.open_file(file_name='model.csv')

with file_handler.get_reader() as f:
    content = f.read()
    
same_content = file_handler.read()
```



### Upload a File or Folder to an Artifact

In addition to uploading a file or folder when an artifact is created, you can also upload files and folders at a later time.

```py
from sapdi.artifact.artifact import Artifact

artifact = Artifact.get(artifact_id='xxxxx-yyyyy-zzzzz')

artifact.upload(local_path='/tmp/artifact/model.csv')
artifact.upload(local_path='/tmp/artifact')
```



### Download Artifact Content

This example downloads the entire content of an artifact to a local directory. A specific file can be downloaded by specifying the `specific_relative_file` argument.

```py
from sapdi.artifact.artifact import Artifact
artifact = Artifact.get(artifact_id='xxxxx-yyyyy-zzzzz')

artifact.download(local_path='/users/myuser')
artifact.download(local_path='/user/myuser', specific_relative_path='text.csv')
```



### Traverse Folders and Files in an Artifact

Folders and files in an artifact whose path is a folder can be traversed in a way similar to traversing the files system using `os.walk`. For example, you can use the following code to print all files \(including files in nested folders\) contained in an artifact.

```py
for dirpath, dirs, filenames in artifact_simple.walk():
    for f_name in filenames:
        print(os.path.join(dirpath, f_name))

```

The traverse can start from a certain subpath within the artifact...

```py
for dirpath, dirs, filenames in artifact_simple.walk(specific_relative_path='subfolder'):
    for f_name in filenames:
        print(os.path.join(dirpath, f_name))

```

...or it can be limited to a certain depth:

```py
for dirpath, dirs, filenames in artifact_simple.walk(depth=1):
    for f_name in filenames:
        print(os.path.join(dirpath, f_name))

```

**Related Information**  


[SDL (Semantic Data Lake)](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/a6b555f56d8c4641bd1a248231202050.html "The SDL connection type connects to and accesses information from remote object stores.") :arrow_upper_right:

