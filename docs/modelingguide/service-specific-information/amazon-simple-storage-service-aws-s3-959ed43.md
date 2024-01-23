<!-- loio959ed43201ba4ef082016cb10e4ade6d -->

# Amazon Simple Storage Service \(AWS S3\)

Many of the SAP Data Intelligence connectors support AWS S3, and there are common characteristics that this service has across the operators.

> ### Note:  
> This topic sometimes refers to an “object” as a “file”, and to an object's “prefix” as a “directory” when the term fits the context of the operator.

AWS S3 is an object store service, which is documented in the [AWS S3](https://docs.aws.amazon.com/s3/) Website.

> ### Restriction:  
> SAP has tested the following services to ensure that they support AWS S3 API: Rook, Minio, and Swift. SAP doesn't guarantee any other service that supports the AWS S3 API to be compatible.



<a name="loio959ed43201ba4ef082016cb10e4ade6d__section_eby_bkh_sfb"/>

## Connection

To use any operator that connects to AWS S3, use a connection ID from the Connection Management application. Set further connection configurations, which aren't in the Connection Management application, described in the following table.


<table>
<tr>
<th valign="top">

Value

</th>
<th valign="top">

Description

</th>
<th valign="top">

Parameters

</th>
</tr>
<tr>
<td valign="top">

Bucket

</td>
<td valign="top">

Optional bucket name to access. The Bucket works as a “fallback” of the connection root path configuration.

> ### Example:  
> If there's no bucket name, in the root path, the value from the Bucket is used.



</td>
<td valign="top">

-   **ID:** awsBucket
-   **Type:**string
-   **Default:** “`com.sap.datahub.test`”



</td>
</tr>
<tr>
<td valign="top">

Proxy

</td>
<td valign="top">

Optional proxy to use in the connection to the service.

</td>
<td valign="top">

-   **ID:** awsProxy
-   **Type:**string
-   **Default:** “”



</td>
</tr>
<tr>
<td valign="top">

Use SSL

</td>
<td valign="top">

Specifies whether to use SSL/TLS when connecting to the service.

</td>
<td valign="top">

-   **ID:** useSSL
-   **Type:**Boolean
-   **Default:** true



</td>
</tr>
</table>



<a name="loio959ed43201ba4ef082016cb10e4ade6d__section_bfv_54h_sfb"/>

## Permissions

Permissions in AWS are required to operate over AWS S3 objects. Each operator can require a determined set of permissions to operate successfully.



### Read File Permissions

To read an object \("file"\) or objects, you need the following permissions:

-   `s3:GetObject` for the given object. See also [AWS S3 GET Object](https://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectGET.html) in the AWS documentation.
-   `s3:GetObjectVersion` for the given object.
-   `s3:ListBucket` to read multiple objects in a prefix \("directory"\). ASW requires the permission for the bucket where the prefix is to be listed.

    > ### Note:  
    > You can narrow the permission to a directory inside the bucket, and the prefix is subject to this restriction. For more information, see [ListBuckets](https://docs.aws.amazon.com/AmazonS3/latest/API/API_ListBuckets.html) in the AWS documentation.

-   `s3:DeleteObject` for the given object when you use *Delete After Send*. For more information, see [DELETE Object](https://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectDELETE.html) in the AWS documentation.



### Write File Permissions

To write an object \("file"\), you need the permission `s3:PutObject` for the bucket to receive the object. For more information, [Policies and Permissions in Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-policy-language-overview.html) in the AWS documentation.

If you use the mode "Append", you also need the permission `s3:GetObject` for the given object. This permission is required because of the write file permission restriction documented in [Restrictions](alibaba-cloud-object-storage-service-oss-6b7c7eb.md#loio6b7c7eb2a990471fb604025327b9fd25__section_qx2_fpl_kjb). For more information, see [GetObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_GetObject.html) in the AWS documentation.



### Remove File Permissions

To remove an object \("file"\), you need the permission `s3:DeleteObject` for the given object. For more information, see [DeleteObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_DeleteObject.html) in the AWS documentation.



### Move File Permissions

Because moving files consists of copying and removing in AWS S3, use the permissions documented in **Remove File Permissions** and **Copy File Permissions** sections.



### Copy File Permissions

To copy an object \("file"\), you need the following permissions:

-   `s3:GetObject` for the source object.

-   `s3:PutObject` for the bucket to receive the copied object.

    If copying by prefix \("directory"\), the operation is bound to the same permissions documented in **Read File Permissions**.




<a name="loio959ed43201ba4ef082016cb10e4ade6d__section_lhn_w13_sfb"/>

## Restrictions



### Directory Restrictions

-   Directories: For a path to be interpreted as a directory, end the path with a forward slash \(`/`\). For example: `/tmp/` is a directory, while `/tmp` is a file named **tmp**.
-   Working directory: Because there's no concept of a "working directory", any relative directory given to or by this service has the root directory \(`/`\) as working directory.



### Write File Restrictions

AWS S3 API doesn't support the "Append" mode. If you use the “Append” mode, the operation retrieves the whole file from the service, and then writes the data back to AWS S3, which compromises the operation's efficiency.



### Move File Restrictions

AWS S3 API doesn't support the “move” operation. If you use the “Move” operation, the operation copies the file and then removes the source file. However, if there's a failure, the operation may copy the file but not remove the source file.



### Copy File Restrictions

Because the “copy” operation has a source and a destination path, the following restrictions apply:

-   If the destination is a file, the source must also be a file.

-   If the destination is a directory, the directory must be empty.


> ### Example:  
> In the give file structure:
> 
> ```
> .
> |
> +-- a
> |   +-- file1.txt
> |   +-- file2.txt
> +-- b
>     +-- f1.txt
>     +-- f2.txt
> ```
> 
> The copy operation has the following results:
> 
> -   Copying source `a/file1.txt` to destination `newfile.txt` succeeds because the destination doesn't exist.
> 
> -   Copying source `a/file1.txt` to destination `b/f1.txt` succeeds and overwrites `b/f1.txt` because the destination is an existing file.
> 
> -   Copying source `a/file1.txt` to destination `b/` fails because `b/` already exists and isn't empty.
> 
> -   Copying source `a/` to destination `b/` fails because `b/` already exists and is empty.
> 
> -   Copying source `a/` to destination `b/dir/` succeeds because `b/dir/` doesn't exist.

**Related Information**  


[Amazon S3 Owner's Page](https://aws.amazon.com/s3/)

