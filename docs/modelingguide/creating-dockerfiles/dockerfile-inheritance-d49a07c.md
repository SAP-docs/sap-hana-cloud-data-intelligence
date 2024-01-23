<!-- loiod49a07c5d66c413ab14731adcfc4f6dd -->

# Dockerfile Inheritance

The Dockerfile inheritance feature in SAP Data Intelligence allows inheriting attributes, such as tags, from other Dockerfiles defined in the Modeler.

It's possible to inherit attributes from other Dockerfiles defined in the Modeler by using the following syntax:

```
docker
FROM $<dockerfile_id>
...
```

Dockerfiles in the Modeler repository each have a corresponding file named `Tags.json`, which is always located in the same directory as the Dockerfile. Along with the software modules used by the Dockerfile, the `Tags.json` file contains the following information about the Dockerfile:

-   Runtimes to use, such as Python.
-   Tools to use, such as Zypper, tar, and gzip.
-   Compilers to use, such as g-cc or gcc+.

The information in the `Tags.json` file allows the Modeler to select the correct Docker image at runtime for the operators and groups in a graph. For more information about Dockerfiles, see [Groups, Tags, and Dockerfiles](../using-graphs/groups-tags-and-dockerfiles-03d1ef5.md).

The Modeler determines whether a child Dockerfile inherits tags from a parent Dockerfile using the criteria in the following table.


<table>
<tr>
<th valign="top">

Tag Origin

</th>
<th valign="top">

Inherited

</th>
<th valign="top">

Not Inherited

</th>
</tr>
<tr>
<td valign="top">

Child Dockerfile \(not in the parent Dockerfile\)

</td>
<td valign="top">

X

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Parent Dockerfile \(not in the child Dockerfile\)

</td>
<td valign="top">

X

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Child and parent Dockerfile \(uses the tag value from the child Dockerfile\)

</td>
<td valign="top">

X

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Parent Dockerfile, marked as special “default”

</td>
<td valign="top">

 

</td>
<td valign="top">

X

</td>
</tr>
</table>

> ### Note:  
> The Modeler never transfers the special tag “default” from the parent to the child Dockerfile, but it still transfers the tag “deprecated”.

> ### Example:  
> To create a new Dockerfile with instructions to install the NumPy library to use in a Python3 operator, use the prebuilt `com.sap.sles.base` Docker image. This Docker image already satisfies the requirements of the Python3 operator. The following code snippet shows the entry in the new Dockerfile:
> 
> ```
> docker
> FROM $com.sap.sles.base
> RUN pip3.9 install numpy
> 
> ```
> 
> For the new Dockerfile, add the tag <code>“numpy39”</code> to the `Tags.json` file located in the same directory as the new Dockerfile:
> 
> ```
> 
> {
>     "numpy39": ""
> }
> 
> ```
> 
> The Modeler expands the new Dockerfile tags automatically to include the tags from the `com/sap/sles/base/Tags.json` file at runtime because of the automatic tags inheritance feature.

> ### Note:  
> For more control over the Docker image, such as installing additional compilers and tools with Zypper, create a Dockerfile that only you control. To create this Dockerfile, SAP includes a Dockerfile template named `org.opensuse` in the repository at `dockerfile/org/opensuse`. Use the template to create a customized copy. For more information about the `org.opensuse` template, see the `README.md` file in the Modeler's navigation pane, under the *Repository* tab: `dockerfiles/org/opensuse/`.

**Added Security**

For security reasons, SAP stopped supporting images that run with a root user in SAP Data Intelligence on-premise version 3.0 and cloud version 2003. Therefore, SAP modified the Docker images to create and use nonroot users. If you own a custom Dockerfile that doesn't inherit from a Dockerfile delivered by SAP, add code to your Dockerfile similar to the following example:

> ### Example:  
> ```
> 
> RUN groupadd -g 1972 vflow && useradd -g 1972 -u 1972 -m vflow
> USER 1972:1972
> WORKDIR /home/vflow
> ENV HOME=/home/vflow
> 
> ```

SAP requires that you use numeric IDs in the `USER` directive instead of the user and group names. If you don't use numeric IDs, the graph doesn't run. Ensure that the commands you execute after the `USER` directive work with the new environment as follows:

-   When you install new Python packages with “pip”, the install must have the “user” flag for local installation.
-   When you install other software without the package managers that support user local installation, you must install the software manually inside your home directory, such as `/home/vflow`. Install any other files added to the image in the same way.

**Related Information**  


[Python3 Operator V2](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/1b5cca1e8f3f418593d042661cc135ad.html "Use the Python3 operator V2 to define a script that offers convenience functions provided by API objects, such as callbacks.") :arrow_upper_right:

