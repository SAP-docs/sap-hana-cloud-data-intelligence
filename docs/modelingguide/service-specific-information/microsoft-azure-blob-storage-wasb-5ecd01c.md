<!-- loio5ecd01cac1524edba05aa4a262e3eeac -->

# Microsoft Azure Blob Storage \(WASB\)

Azure Storage Blob \(WASB\) is one of Microsoft's cloud storage services. Additional information, including the documentation, can be found at the official WASB homepage.

Many of the SAP Data Intelligence storage operators offer support for WASB. This documentation covers the common characteristics that this service has across operators.

This document may refer to an object as a "file" and to an object's prefix as a "directory" if it fits the context of the operator.



<a name="loio5ecd01cac1524edba05aa4a262e3eeac__section_eby_bkh_sfb"/>

## Connection

To use any operator that connects to WASB, you may use a Connection ID from the Connection Management.

Further connection configurations may be set, which are not in the Connection Management:

-   Container. Optional container name to be accessed. It works as a "fallback" of the Connection's Root Path configuration. For example, if no bucket is given in the Root Path, the value from Container is used.
    -   ID: `containerName`
    -   Type: `string`
    -   Default: "mycontainer"

-   Blob Type. Only used in Write File operator. It sets the blob type of the destination blob \("file"\).
    -   ID: `wasbBlobType`

        Type: `string`

        Default: "BlockBlob"

    -   Values:
        -   "BlockBlob"
        -   "PageBlob"
        -   "AppendBlob"





<a name="loio5ecd01cac1524edba05aa4a262e3eeac__section_ody_v4p_sfb"/>

## Permissions

Permissions in Azure Blob Storage are required to operate over blobs. WASB currently restricts access to blobs through the container's policy:

-   Full public read access
-   Public read access for blobs only
-   No public read access

Learn more at [Set Container ACL](https://docs.microsoft.com/en-us/rest/api/storageservices/set-container-acl) and [Authorize requests to Azure Storage](https://docs.microsoft.com/en-us/rest/api/storageservices/authorization-for-the-azure-storage-services).

Operators will need full access to the data, thus the container should have "Full public read access" if the given credentials are not from the owner of the container; otherwise, any permission should be enough.



<a name="loio5ecd01cac1524edba05aa4a262e3eeac__section_lhn_w13_sfb"/>

## Restrictions

-   Directories. For a path to be interpreted as a directory, it should end with `/`. For example: `/tmp/` is a directory, while `/tmp` is a file named `tmp`.
-   Working directory. Because there is no concept of a "working directory", any relative directory given to or by this service will have the root directory \(`/`\) as working directory.



### Move File Restrictions

As the WASB API does not support the move operation, the operation consists of a copy followed by removing the source file. Thus, in cases of failure, the file may be copied and not removed.



### Copy File Restrictions

Given that the operation has a "source" and a "destination" path:

-   If the destination is a file, source must also be a file.
-   If the destination is a directory, it must be empty.

For instance, consider this file structure:

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

-   Copying the source `a/file1.txt` to the destination `newfile.txt` would succeed because the destination does not exist.
-   Copying the source `a/file1.txt` to the destination `b/f1.txt` would succeed and overwrite `b/f1.txt` because the destination is an existing file.
-   Copying the source `a/file1.txt` to the destination: `b/` would fail because `b/` already exists and is not empty.
-   Copying the source `a/` to the destination `b/` would fail because `b/` already exists and is not empty.
-   Copying the source `a/` to the destination `b/dir/` would succeed because `b/dir/` does not exist.

**Related Information**  


[Official WASB Homepage](https://azure.microsoft.com/en-us/services/storage/blobs/)

