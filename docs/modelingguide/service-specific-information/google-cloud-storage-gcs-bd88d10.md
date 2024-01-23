<!-- loiobd88d109721146a684cb47462864ccde -->

# Google Cloud Storage \(GCS\)

GCS is Google's Object Storage cloud service. Additional information, including the documentation, can be found at the official GCS Homepage.

Many of the Storage operators offer support for GCS. This documentation regards the common characteristics that this service has across operators.

This document may refer to an object as a "file", and to an object's prefix as a "directory", if it fits the context of the operator.



<a name="loiobd88d109721146a684cb47462864ccde__section_eby_bkh_sfb"/>

## Connection

> ### Note:  

In order to use any operator that connects to GCS, you may use a Connection ID from the Connection Management.

Further connection configurations may be set, which are not in the Connection Management. Such as:

-   Bucket

    Optional bucket name to be accessed. It works as a "fallback" of the Connection's Root Path configuration. For instance, if no bucket is given in the Root Path, the value from Bucket is used.

    -   ID: `gcsBucket`

    -   Type: `string`

    -   Default: "bucket"


-   Content Type

    Informs the type of data being sent, allowing the correct rendering of objects. For instance, if you send a JSON file, this should be set to application/json. Additional information here:[Working With Object Metadata](https://cloud.google.com/storage/docs/gsutil/addlhelp/WorkingWithObjectMetadata).

    -   ID: `gcsContentType`

        Type: `string`

        Default: ""





<a name="loiobd88d109721146a684cb47462864ccde__section_bfv_54h_sfb"/>

## Permissions

[GCS Permissions](https://cloud.google.com/storage/docs/access-control/) for manipulating objects are described in the [Access Control List](https://cloud.google.com/storage/docs/access-control/lists#permissions) documentation as WRITER, READER and OWNER. Each operator may require a determined set to successfully operate.



### Read File Permissions

To read a single object \("file"\), you need `READER` and `WRITER` permissions on the bucket.



### Write File Permissions

To write an object \("file"\), you need `WRITER` permission on the bucket.



### Remove File Permissions

To remove an object \("file"\), you need the `READER` and `WRITER` permissions on the bucket.



### Move File Permissions

To move an object \("file"\), you need the `READER` and `WRITER` permissions on the origin bucket plus the `READER` and `WRITER` permissions on the destination bucket.



### Copy File Permissions

To copy an object \("file"\), you need the `READER` permission on the origin bucket, plus the `READER` and `WRITER` permission on the destination bucket.



<a name="loiobd88d109721146a684cb47462864ccde__section_lhn_w13_sfb"/>

## Restrictions

-   Directories:

    In order for a path to be interpreted as a directory, it should end with `/`. For example: `/tmp/` is a directory, while `/tmp` is a file named `tmp`.

-   Working directory:

    Since there is no concept of a "working directory", any relative directory given to/by this service will have the root directory \(`/`\) as working directory.




### Move File Restrictions

As the GCS API does not support the move operation, the operation consists of a copy followed by removing the source file. Thus, in cases of failure, the file may be copied and not removed.



### Copy File Restrictions

Taking that the operation has a "source" and a "destination" path:

-   If the destination is a file, source must also be a file.

-   If the destination is a directory, it must be empty.


For instance, in the given file structure:

```
.
|
+-- a
|   +-- file1.txt
|   +-- file2.txt
+-- b
    +-- f1.txt
    +-- f2.txt
```

-   Copying source: `a/file1.txt` to destination: `newfile.txt`, would succeed, since the destination does not exist.

-   Copying source: `a/file1.txt` to destination: `b/f1.txt`, would succeed and overwrite `b/f1.txt`, since the destination is an existing file.

-   Copying source: `a/file1.txt` to destination: `b/`, would fail, since `b/` already exists and is not empty.

-   Copying source: `a/` to destination: `b/` would fail, since `b/` already exists and is not empty.

-   Copying source: `a/` to destination: `b/dir/` would succeed, since `b/dir/` does not exist.


**Related Information**  


[Official GCS Documentation](https://cloud.google.com/storage/)

