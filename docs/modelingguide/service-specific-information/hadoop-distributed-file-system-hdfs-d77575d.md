<!-- loiod77575d3b41f41ef8eee5ade46ff7d84 -->

# Hadoop Distributed File System \(HDFS\)

Hadoop Distributed File System is Apache's distributed storage solution. For more information, see the official HDFS documentation.

> ### Note:  
> Some configurations are only supported with connections defined via Connection Management.

Many of the SAP Data Intelligence storage operators offer support for HDFS. This documentation covers the common characteristics that this service has across operators.



<a name="loiod77575d3b41f41ef8eee5ade46ff7d84__section_wxb_lh4_sfb"/>

## Connection

In order to use any operator that connects to HDFS, you may use a Connection ID from the Connection Management.



<a name="loiod77575d3b41f41ef8eee5ade46ff7d84__section_bfv_54h_sfb"/>

## Permissions

The [HDFS Permissions](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html) for files and directories are based on the POSIX model, that is, for each file or directory there are W, R and X permissions that may be attributed separately to the owner, the group associated with the file/directory and the group of remaining users.

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




<a name="loiod77575d3b41f41ef8eee5ade46ff7d84__section_epz_xph_sfb"/>

## Restrictions

-   Working directory:

    Since there is no concept of a "working directory", any relative directory given to/by this service will have the root directory \(/\) as working directory.




### Copy File Restrictions

Since the HDFS API does not support the copy operation, this behavior can be achieved through `Read + Write`.

**Related Information**  


[Official HDFS Documentation](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html)

