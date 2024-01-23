<!-- loio4d4da2140f354ba09fa4a280527f6e07 -->

# List Files V2

The List Files operator lists files and directories from various storage services.



A list operation happens according to the *List* configuration. `On input` means the input contains the path to be listed. `Once` tells the operator to take the path from the configuration.

The operator gets its connection according to the *Connection* property. You can set *Connection type* to `From input` only when reading `On input`. Otherwise, a static connection ID from `Connection Management` can be used.

Each file to be listed will generate an output. More details are in the Output section below.

Supported services are:

-   Alibaba Cloud Object Storage Service \(OSS\).

-   Amazon Simple Storage Service \(S3\).

    > ### Note:  
    > Also supports S3-compatible services.

-   Google Cloud Storage \(GCS\).
-   Hadoop Distributed File System \(HDFS\).
-   HANA Data Lake \(HDL\_FILES\).
-   Microsoft Azure Data Lake \(ADL\).
-   Microsoft Azure Data Lake Gen. 2 \(ADL\_V2\).
-   Microsoft Windows Azure Storage Blobs \(WASB\).
-   Semantic Data Lake \(SDL\).
-   SSH File Transfer Protocol \(SFTP\).
-   Local File System .

    > ### Note:  
    > It does not use a Connection ID. It is the local file system of the environment in which the group containing this operator is running. Operators in a different group don't have access to it. Accessing any file or folder under the path `/vrep` is not supported and, while the operator may still run with such a configured path, it is unadvised.




<a name="loio4d4da2140f354ba09fa4a280527f6e07__section_uzd_jyk_ntb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

ID

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

List

</td>
<td valign="top">

mode

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The operation mode. Find details of each mode below.

-   `On input`: a list operation happens for every input received. The input informs the path to list from.

-   `Once`: a single list operation happens as soon as the graph is`Running`. The *Path* configuration informs the path to list from.

Default: `"On input"`

</td>
</tr>
<tr>
<td valign="top">

Connection \(static\)

</td>
<td valign="top">

connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Points to the static connection to list from. Only available if *List* is set to `Once`.

Default: `{}`

</td>
</tr>
<tr>
<td valign="top">

Connection \(dynamic\)

</td>
<td valign="top">

dynamicConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Points to the dynamic connection to list from. It uses the file connection attribute. Only available if *List* is set to `On input`.

Default: `{"configurationType":"From input"}`

</td>
</tr>
<tr>
<td valign="top">

Path

</td>
<td valign="top">

path

</td>
<td valign="top">

string

</td>
<td valign="top">

Points to the directory to list files from, relative to the used connection. It must be in the qualified name format. If the *Connection* is set with a connection ID, you may use the UI file browsing to set the path. Only available if *List* is set to `Once`.

Default: `/`

</td>
</tr>
<tr>
<td valign="top">

Recursive

</td>
<td valign="top">

recursive

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Whether to browse through subdirectories recursively. If false, only the files and directories at the first level of the requested path are listed.

Default: `false`

</td>
</tr>
<tr>
<td valign="top">

List Directories

</td>
<td valign="top">

listDirectories

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Whether to list directories. If false, only files are listed. Otherwise, both are listed.

Default: `false`

</td>
</tr>
<tr>
<td valign="top">

Treat Part File Directory As

</td>
<td valign="top">

identifyPartFiles

</td>
<td valign="top">

string

</td>
<td valign="top">

Lists directories with [Partitioned Files](partitioned-files-34eab43.md) format as a single file or as a directory. See the section **Examples with Part Files** for examples.

Accepted values:

-   File: the part file directory will be listed as a file, with \`isDir\` set to false. If *Recursive* is set, the operator will not list the files inside the part file directory.

-   Directory: the part file directory will be listed as any other directory.

    > ### Note:  
    > if no part file directories are expected, it's recommended to set this configuration to *Directory* to better performance.


Default: File

</td>
</tr>
<tr>
<td valign="top">

Skip Part File Without Success File

</td>
<td valign="top">

skipOngoingPartFile

</td>
<td valign="top">

string

</td>
<td valign="top">

Chooses to list directories part file directories without the success file like a single file, a directory, or to skip them. If set to *Treat as directory* or *Ignore*, an ongoing part file will not be treated as a part file. See the section **Examples with Part Files** for examples.

-   Ignore: an ongoing part file and the files inside the directory, if *Recursive* is set, will not be listed.

-   Treat as directory: all ongoing part files will be treat as non part file directories.
-   Treat as file: all ongoing part files directories will be treated as part files.

Default: Ignore

</td>
</tr>
<tr>
<td valign="top">

Filter

</td>
<td valign="top">

filter

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Sets a specific filter for outputs.

Accepted values:

-   `None`: no filter is used. All outputs occur normally.

-   `With regular expression`: only names that match the regular expression epecified in *Pattern* are sent as output.

Default: `"None"`

</td>
</tr>
<tr>
<td valign="top">

Pattern

</td>
<td valign="top">

pattern

</td>
<td valign="top">

string

</td>
<td valign="top">

The regular expression used to filter outputs. Only names that match the expression are sent as output.

It uses the RE2 standard: [https://github.com/google/re2/wiki/Syntax](https://github.com/google/re2/wiki/Syntax).

Default: `""`

</td>
</tr>
<tr>
<td valign="top">

Error Handling

</td>
<td valign="top">

errorHandling

</td>
<td valign="top">

string

</td>
<td valign="top">

Details available at [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:.

Default: `"terminate on error"`

</td>
</tr>
</table>



<a name="loio4d4da2140f354ba09fa4a280527f6e07__section_yzz_fbl_ntb"/>

## Input


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Kind

</th>
<th valign="top">

Type ID

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

dirRef

</td>
<td valign="top">

none

</td>
<td valign="top">

""

</td>
<td valign="top">

An input with an empty body and the header `com.sap.headers.file`, whose field `path` points to the directory to list. If it points to a file, the operator forwards it to the output. When *Connection \(dynamic\)* is set to `From input`, the field `connection` must specify the connection to be used.

</td>
</tr>
</table>



<a name="loio4d4da2140f354ba09fa4a280527f6e07__section_ajk_qbl_ntb"/>

## Output


<table>
<tr>
<th valign="top">

Output

</th>
<th valign="top">

Kind

</th>
<th valign="top">

Tupe ID

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

ref

</td>
<td valign="top">

none

</td>
<td valign="top">

""

</td>
<td valign="top">

An output with an empty body and the header `com.sap.headers.file` set with the metadata of the file listed. Each file to be listed will generate an output.

</td>
</tr>
<tr>
<td valign="top">

error

</td>
<td valign="top">

structure

</td>
<td valign="top">

com.sap.error

</td>
<td valign="top">

An error message as described at [Error Handling in Generation 2 Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/b88468d2f3184b9098164cfde2af1d8c.html "The SAP Data Intelligent Modeler reports errors to a dedicated operator through an error output port.") :arrow_upper_right:. It depends on the *Error Handling* configuration.

</td>
</tr>
</table>



<a name="loio4d4da2140f354ba09fa4a280527f6e07__section_ntx_dtl_3vb"/>

## Snapshot Support

Snapshot support is provided when *List* is set to *Once*, with *at-least-once* guarantee.

The state is saved between outputs, so, upon recovery, the operator doesn't have to start listing the files from scratch.

Instead, once the graph is resumed, the list starts from the last batch index saved. For the list operation to work properly when resuming or restoring a graph, the directory content must not change since the last execution. Otherwise, it's not guaranteed that all files will be listed.



<a name="loio4d4da2140f354ba09fa4a280527f6e07__section_ndh_3tl_3vb"/>

## Examples with Part Files

Consider the file structure below, which contains some part files:

```
myDirectory/
  file1.txt
  subdir1/
    file2.txt
  partFile1.csv/
    _SUCCESS
    part-0000-1.csv
    part-0000-2.csv
  incompletePartFile.txt/
    part-0123-1.txt
  subdir2/
    partFile2.csv/
      _SUCCESS
      part-abcd-1.csv
      part-abcd-2.csv
```

The following examples show the expected output when the operator lists "myDirectory" with determined configurations:

> ### Example:  
> ```
> Operator configuration:
>   Recursive: false
>   List directories: false
>   Treat part file directory as: File
>   Skip part file without success file: Treat as file
> 
> Listed Files:
>   file1.txt                 isDir: false 
>   partFile1.csv             isDir: false
>   incompletePartFile.txt    isDir: false
> ```

> ### Example:  
> ```
> Operator configuration:
>   Recursive: false
>   List directories: true
>   Treat part file directory as: File
>   Skip part file without success file: Treat as directory
> 
> Listed Files:
>   file1.txt                 isDir: false
>   subdir1                   isDir: true 
>   partFile1.csv             isDir: false
>   incompletePartFile.txt    isDir: true
>   subdir2                   isDir: true
> ```

> ### Example:  
> ```
> Operator configuration:
>   Recursive: true
>   List directories: true
>   Treat part file directory as: File
>   Skip part file without success file: Ignore
> 
> Listed Files:
>   file1.txt                 isDir: false
>   subdir1                   isDir: true
>   subdir1/file2.txt         isDir: false 
>   partFile1.csv             isDir: false
>   subdir2                   isDir: true
>   subdir2/partFile2.csv     isDir: false
> ```

> ### Example:  
> ```
> Operator configuration:
>   Recursive: true
>   List directories: false
>   Treat part file directory as: File
>   Skip part file without success file: Treat as directory
> 
> Listed Files:
>   file1.txt                                 isDir: false
>   subdir1/file2.txt                         isDir: false 
>   partFile1.csv                             isDir: false
>   incompletePartFile.txt/part-0123-1.txt    isDir: false
>   subdir2/partFile2.csv                     isDir: false
> ```

> ### Example:  
> ```
> Operator configuration:
>   Recursive: false
>   List directories: true
>   Treat part file directory as: Directory
>   Skip part file without success file: -
> 
> Listed Files:
>   file1.txt                 isDir: false
>   subdir1                   isDir: true 
>   partFile1.csv             isDir: true
>   incompletePartFile.txt    isDir: true
>   subdir2                   isDir: true
> ```

> ### Example:  
> ```
> Operator configuration:
>   Recursive: true
>   List directories: false
>   Treat part file directory as: Directory
>   Skip part file without success file: -
> 
> Listed Files:
>   file1.txt                                 isDir: false
>   subdir1/file2.txt                         isDir: false 
>   partFile1.csv/_SUCCESS                    isDir: false
>   partFile1.csv/part-0000-1.csv             isDir: false
>   partFile1.csv/part-0000-2.csv             isDir: false
>   incompletePartFile.txt/part-0123-1.txt    isDir: false
>   subdir2/partFile2.csv/_SUCCESS            isDir: false
>   subdir2/partFile2.csv/part-abcd-1.csv     isDir: false
>   subdir2/partFile2.csv/part-abcd-2.csv     isDir: false
> ```

