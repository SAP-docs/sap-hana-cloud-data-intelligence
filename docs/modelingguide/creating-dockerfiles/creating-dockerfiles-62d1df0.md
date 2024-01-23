<!-- loio62d1df08fa384d0e88bbe9b7cbd2c3fb -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Creating Dockerfiles

Dockerfiles contain all commands that you call on a command line to assemble a docker image.



<a name="loio62d1df08fa384d0e88bbe9b7cbd2c3fb__context_fhx_nl4_dbb"/>

## Context

In the Modeler application, you can create a library of Dockerfiles. Dockerfiles provide a predefined runtime environment to run the operators in a graph \(pipeline\). The Modeler stores Dockerfiles in the repository in a Dockerfile folder.



<a name="loio62d1df08fa384d0e88bbe9b7cbd2c3fb__steps_ghx_nl4_dbb"/>

## Procedure

1.  Open the *Repository* tab in the navigation pane of the Modeler application.

2.  Create a folder.

    1.  Right-click the Dockerfiles category folder and choose *Create Folder*.

    2.  Enter a name for the root folder in *Name your folder* text box and select *Create*.

        > ### Note:  
        > To create a folder structure \(subdirectories\) in the root folder, create a new folder in a subdirectory under the dockerfiles folder.

        The Modeler creates a new folder in which you create a Dockerfile.


3.  Create a Dockerfile.

    1.  Right-click the folder in which to create the Docker file and choose *Create Docker File*.

    2.  Enter a name in *Name*.

    3.  Choose *OK*.

    4.  In the editor, write the script that defines your Dockerfile.

        > ### Note:  
        > For security reasons, SAP recommends that you start the image with the non-root user.


4.  Create tags.

    Tags describe the runtime requirements of operators and are the annotations of Dockerfiles that you create.

    1.  In the editor toolbar, choose <span class="SAP-icons"></span> \(Show Configuration\).

    2.  In the Configuration pane, choose :heavy_plus_sign:

    3.  Choose a tag from the first text box list.

    4.  Enter a version in the second text box.


5.  In the editor toolbar, choose :floppy_disk:

6.  Build a docker image.

    1.  In the editor toolbar, choose :arrow_forward: to build a docker image for the Dockerfile.

    2.  **Optional:** Select :arrow_forward: in the editor toolbar.

        *Force Build* rebuilds the existing Docker image. The Modeler finds changes in the Docker image and rebuilds based on the changes.





<a name="loio62d1df08fa384d0e88bbe9b7cbd2c3fb__postreq_l41_yhp_tjb"/>

## Next Steps

For security reasons, the Modeler application has stopped supporting images that run with a root user.

```
RUN groupadd -g 1972 vflow && useradd -g 1972 -u 1972 -m vflow
USER 1972:1972
WORKDIR /home/vflow
ENV HOME=/home/vflow
```

> ### Restriction:  
> Use numeric IDs in the USER directive instead of using group names. Otherwise the graph run fails.

Make sure that the commands you run after the USER directive operate with the new environment. Therefore, consider the following situations:

-   If you install new Python packages with `pip`, ensure that you have the `--user` flag for local installations.
-   If you install software without using the package manager, or you install software that doesn't support local installation, then you must install the software manually inside the user home directory, such as `/home/vflow`. Do the same for any other files added to the image.

-   **[Dockerfile Inheritance](dockerfile-inheritance-d49a07c.md "The Dockerfile inheritance feature in SAP Data Intelligence allows inheriting attributes, such as tags, from other Dockerfiles defined in
		the Modeler. ")**  
The Dockerfile inheritance feature in SAP Data Intelligence allows inheriting attributes, such as tags, from other Dockerfiles defined in the Modeler.
-   **[Referencing Parent Docker Images](referencing-parent-docker-images-d9a3063.md " To create a new Docker image, SAP Data Intelligence Modeler allows you to reference a parent Docker image, which can be an existing
		Dockerfile from the repository or a prebuilt Docker image. ")**  
 To create a new Docker image, SAP Data Intelligence Modeler allows you to reference a parent Docker image, which can be an existing Dockerfile from the repository or a prebuilt Docker image.

