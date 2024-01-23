<!-- loioe78850b420ec41728036e6bc01f4535f -->

# Microsoft Azure Data Lake \(ADL\)

Azure Data Lake \(ADL\) is Microsoft's Data Lake cloud storage service. Additional information, including the documentation, can be found at the official ADL Homepage.

Many of the SAP Data Intelligence storage operators offer support for ADL. This documentation covers the common characteristics that this service has across operators.



<a name="loioe78850b420ec41728036e6bc01f4535f__section_eby_bkh_sfb"/>

## Connection

In order to use any operator that connects to ADL, you may use a Connection ID from the Connection Management.



<a name="loioe78850b420ec41728036e6bc01f4535f__section_bfv_54h_sfb"/>

## Permissions

The ADL interface is based on the WebHDFS service, thus the [ADL Permissions](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-access-control) for files and directories are based on the POSIX model, that is, for each file or directory there are W, R and X permissions that may be attributed separately to the owner, the group associated with the file/directory and the group of remaining users.

For a finer control, it is possible to define an [Access Control List](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists), which allows the definition of specific rules for each user or each group of users.



### Read File Permissions

To read a file, you need `W` and `R` permissions on the file.



### Write File Permissions

To write a new file, you need `W` permission on the directory where the file will be created.

To append or overwrite an existing file, you need `W` permission on the file.



### Remove File Permissions

To remove a file or directory, you need `W` and `R` permissions on the corresponding file/directory.



### Move File Permissions

-   Moving a File:

    To move a file you need `W` permission on the original file and `R` permission on the original directory.

    If the destination file already exists and is being overwritten, you need `W` permission on the destination file.

    On the other hand, if the file does not exist on the destination, you need `W` permission on the destination directory.

-   Moving a Directory:

    To move a directory, you need `W` and `R` permissions on the original directory and `W` permission on every file within it.

    On the destination folder, you need `W` permission.

    If any of the files already exist at the destination and needs to be overwritten, you need the `W` permission on the destination file as well.




<a name="loioe78850b420ec41728036e6bc01f4535f__section_epz_xph_sfb"/>

## Restrictions

-   Working directory: Because there is no concept of a "working directory," any relative directory given to or used by this service will have the root directory \(/\) as its working directory.
-   Copying: Because the ADL API does not support the copy operation, this behavior can be achieved through `Read + Write`.

**Related Information**  


[Official ADL Homepage](https://azure.microsoft.com/en-us/solutions/data-lake/)

