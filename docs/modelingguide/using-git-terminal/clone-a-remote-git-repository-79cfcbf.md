<!-- loio79cfcbff4ee14bf2a9b13969aa6db423 -->

# Clone a Remote Git Repository



<a name="loio79cfcbff4ee14bf2a9b13969aa6db423__prereq_i3c_d4b_rwb"/>

## Prerequisites

Before you perform this task, ensure that you've completed the following tasks:

-   Configure credential handling by following the process in [Git Credential Handling Using Standard Git Credential Helper](git-credential-handling-using-standard-git-credential-helper-d5d6805.md).
-   Create a local Git repository by following the process in [Create a Local Git Repository](create-a-local-git-repository-27c6f55.md).

Also ensure the following:

-   The workspace of the user of the Git terminal application in SAP Data Intelligence Cloud is empty.
-   You have the appropriate permissions to access the Git terminal in the Modeler application.

    > ### Note:  
    > If you don't see the *Git Terminal* tab in the lower pane of the Modeler, request the applicable permission from your administrator.




## Context

> ### Caution:  
> The following steps are to introduce the process for a cloning a remote Git repository. The success of the example command sequences depends on the actual folder structure of the remote Git repository, or additional design time artifacts that are stored in your user workspace.

To clone a remote Git repository, perform the following steps:



## Procedure

1.  Open the *Git Terminal* tab in the lower pane of the Modeler.

    A Git terminal opens in the tab.

2.  Type the following command into the Git terminal:

    ```
    # configure user E-Mail and user name for the local gitrepository 
    git clone https://<url>/to/remote_repository.git .
    
    ```

    > ### Note:  
    > The dot at the end of this command causes the Git command-line client to clone the repository content to the root folder of the user workspace \(`vhome`\) instead of cloning the content to a subfolder \(`vhome/.remote_repository`\).




<a name="loio79cfcbff4ee14bf2a9b13969aa6db423__result_bcg_szb_rwb"/>

## Results

Because the folder structure in the remote Git repository is similar to the following structure, SAP Data Intelligence recognizes the `graph.json`, and you can run the graph or manipulate its content directly:

```

vflow/
		graphs
				demo-graph
		operators
		dockerfiles
		subdevkits
		subengines		
```

