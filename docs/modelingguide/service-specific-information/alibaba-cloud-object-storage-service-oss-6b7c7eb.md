<!-- loio6b7c7eb2a990471fb604025327b9fd25 -->

# Alibaba Cloud Object Storage Service \(OSS\)

Many of the SAP Data Intelligence storage operators support the Alibaba Cloud OSS, and there are common characteristics that this service has across the operators.

> ### Note:  
> This topic sometimes refers to an “object” as a “file”, and to an object's “prefix” as a “directory” when the term fits the context of the operator.



<a name="loio6b7c7eb2a990471fb604025327b9fd25__section_rqk_jml_kjb"/>

## Connection

To use any operator that connects to Alibaba OSS, either use a connection ID \(Connection Management application\) or set a manual connection using the values in the following table.


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

Endpoint

</td>
<td valign="top">

**Required.** Allows using an endpoint to access Alibaba Cloud OSS.

</td>
<td valign="top">

-   **ID:** endpoint
-   **Type:**string
-   **Default:** “`oss-cn-hangzhou.aliyuncs.com`”



</td>
</tr>
<tr>
<td valign="top">

Protocol

</td>
<td valign="top">

**Required.** Sets the protocol to use. This value overwrites the protocol prefixed in the endpoint configuration, if any.

</td>
<td valign="top">

-   **ID:** Protocol
-   **Type:**string
-   **Default:** “HTTPS”

    Possible values include “HTTP” or “HTTPS”.




</td>
</tr>
<tr>
<td valign="top">

Region

</td>
<td valign="top">

The Alibaba Cloud region to which the configured bucket belongs. The bucket name is in the root path.

</td>
<td valign="top">

-   **ID:** region
-   **Type:**string
-   **Default:** “`oss-cn-hangzhou`”



</td>
</tr>
<tr>
<td valign="top">

Access Key

</td>
<td valign="top">

**Required.** The Access Key ID to authenticate to the service. To authenticate, the Access Key ID pairs with the Secret Key.

</td>
<td valign="top">

-   **ID:** accessKey
-   **Type:**string
-   **Default:** “`OSSAccessKeyID`”



</td>
</tr>
<tr>
<td valign="top">

Secret Key

</td>
<td valign="top">

**Required.** The Secret Key to authenticate to the service. To authenticate, the Secret Key pairs with the Access Key.

</td>
<td valign="top">

-   **ID:** secretKey
-   **Type:**string
-   **Default:** “”



</td>
</tr>
<tr>
<td valign="top">

Root Path

</td>
<td valign="top">

The bucket name and an optional root path name for browsing. The path starts with a forward slash \(/\) and then the bucket name. Optionally add another forward slash and the root path.

> ### Example:  
> <code>/<i class="varname">&lt;MyBucket&gt;</i>/<i class="varname">&lt;My Folder&gt;</i></code>

Dataset names for this connection don't contain segments of the rootPath; instead, the first segment of the dataset is a subdirectory of the root path.

</td>
<td valign="top">

-   **ID:** rootPath
-   **Type:**string
-   **Default:** “<code>/<i class="varname">&lt;MyBucket&gt;</i>/<i class="varname">&lt;My Folder&gt;</i></code>”



</td>
</tr>
</table>



<a name="loio6b7c7eb2a990471fb604025327b9fd25__section_tft_jnl_kjb"/>

## Permissions

Permissions in Alibaba Cloud are required to operate over Alibaba Cloud OSS objects. For more information, see [Access and Control](https://www.alibabacloud.com/help/en/oss/user-guide/access-and-control/?spm=a2c63.p38356.0.0.36b87fdf5IYJmA) in the Alibaba Cloud OSS documentation.

Alibaba OSS provides an Access Control List \(ACL\) for bucket-level access control. One of the following permissions are required:

-   public-read-write

-   public-read

-   private


For descriptions of the permissions, see [ACL types](https://www.alibabacloud.com/help/en/oss/user-guide/bucket-acl-2) in the Alibaba Cloud OSS documentation.

If you don't set an ACL for a bucket when you create it, the bucket's ACL is set to private automatically. If the ACL rule of the bucket is set to private, only authorized users can access and operate on objects in the bucket. To authorize other users to access your Alibaba Cloud OSS resources, refer to [Bucket Policy](https://www.alibabacloud.com/help/en/oss/user-guide/overview#concept-ahc-tx4-j2b) in the Alibaba Cloud OSS documentation.



### Read File Permissions

To read a single object \("file"\), you need the permission `oss:GetObject` for the given object. For more information, see [GetObject](https://www.alibabacloud.com/help/en/oss/developer-reference/getobject#reference-ccf-rgd-5db) in the Alibaba Cloud OSS documentation.

To read multiple objects in a prefix \("directory"\), you need the permission `oss:GetBucket` for the bucket where the prefix is to be listed. The permission can be narrowed to a directory inside the bucket, and the prefix is subject to this restriction. For more information, see [GetBucket \(ListObjects\)](https://www.alibabacloud.com/help/en/oss/developer-reference/listobjects) in the Alibaba Cloud OSS documentation.



### Write File Permissions

To write an object \("file"\), you need the permission `oss:PutObject` for the bucket to receive the object.

If using mode "Append", you also need `oss:GetObject` for the given object.



### Remove File Permissions

To remove an object \("file"\), you need the permission `oss:DeleteObject` for the given object.



### Move File Permissions

Because moving consists of copying and removing in Alibaba Cloud OSS, you need the permissions documented in **Remove File Permissions** and **Copy File Permissions**.



### Copy File Permissions

To copy an object \("file"\), you need the following permissions:

-   `oss:GetObject` for the source object.

-   `oss:PutObject` for the bucket to receive the copied object.


For more information, see [Alibaba Cloud OSS Multipart Upload Operations documentation](https://www.alibabacloud.com/help/doc-detail/31991.htm?spm=a2c63.p38356.b99.830.12624ce0ZP9QZy).

If copying by prefix \( "directory"\), the operation is bound to the same permissions documented in **Read File Permissions**.



<a name="loio6b7c7eb2a990471fb604025327b9fd25__section_qx2_fpl_kjb"/>

## Restrictions



### Directory Restrictions

-   Directories: For a path to be interpreted as a directory, end the path with a forward slash \(`/`\). For example: `/tmp/` is a directory, while `/tmp` is a file named **tmp**.

-   Working directory: Because there's no concept of a "working directory", any relative directory given to or by this service has the root directory \(`/`\) as working directory.




### Write File Restrictions

Alibaba Cloud OSS API doesn't support the “Append” mode. If you use the “Append” mode, the operation retrieves the whole file from the service and then writes the data back to OSS, which compromises the operation's efficiency.



### Move File Restrictions

Alibaba Cloud OSS API doesn't support the “move” operation. If you use the move operation, the operation copies the file and then removes the source file. However, if there's a failure, the operation may copy the file but not remove the source file.



### Copy File Restrictions

Because the “copy” operation has a source and a destination path, the following restrictions apply:

-   If the destination is a file, the source must also be a file.

-   If the destination is a directory, the directory must be empty.


> ### Example:  
> In the given file structure:
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
> -   Copying source `a/file1.txt` to destination `b/f1.txt` succeeds and overwrites `b/f1.txt`, because the destination is an existing file.
> 
> -   Copying source `a/file1.txt` to destination: `b/` fails because `b/` already exists and is empty.
> 
> -   Copying source `a/` to destination `b/` fails because `b/` already exists and isn't empty.
> 
> -   Copying source `a/` to destination `b/dir/` succeeds because `b/dir/` doesn't exist.

**Related Information**  


[Alibaba Cloud's Official Website](https://www.alibabacloud.com/product/oss)

