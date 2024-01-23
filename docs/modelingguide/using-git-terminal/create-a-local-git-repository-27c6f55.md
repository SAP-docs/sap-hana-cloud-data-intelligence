<!-- loio27c6f55194054dfcbd1983ee272948ec -->

# Create a Local Git Repository

Use the Git Terminal in the SAP Data Intelligence Modeler application to create a local Git repository, then push the graph to your remote Git repository location.



<a name="loio27c6f55194054dfcbd1983ee272948ec__prereq_qgx_ykb_rwb"/>

## Prerequisites

Before you perform this task, ensure that you configure credential handling. For information about configuring credential handling, see [Git Credential Handling Using Standard Git Credential Helper](git-credential-handling-using-standard-git-credential-helper-d5d6805.md).

Ensure that you have the appropriate permissions to create a local Git repository in SAP Data Intelligence.

> ### Note:  
> If you don't see the *Git Terminal* tab in the lower pane of the Modeler, request the applicable permission from your administrator.



## Context

> ### Caution:  
> The following steps are to introduce the process for a basic creation of a local Git repository. The success of the example command sequences depends on the actual folder structure of the remote Git repository, or additional design time artifacts that are stored in your user workspace.

To create a local Git repository, perform the following steps in the Modeler application:



## Procedure

1.  Create a graph using the following folder structure:

    `files/vflow/graphs/demo-graph`

2.  Open the *Git Terminal* tab in the lower pane of the Modeler.

    A Git terminal opens in the tab.

3.  Type the following code in the Git terminal:

    ```
    # init git repository and set the name of the default branch to 
    # 'main'
    git init -b main
    
    # configure user E-Mail and user name for the local git #repository 
    git config user.email “<replace with email>”
    git config user.name “<replace with user name>”
    
    # add the demo-graph to the git staging area
    git add vflow/graphs/demo-graph/graph.json
    
    # commit the changes to the local Git repository 
    git commit -m “add demo graph”
    
    ```

    This code creates the local Git repository.

4.  Type the following code in the Git terminal, replacing <code>https://<i class="varname">&lt;url&gt;</i>/to/remote_repository.git</code> with the actual address to the remote Git repository:

    ```
    # add the address to the remote Git repository to the local Git 
    # repository 
    git remote add origin https://<url>/to/remote_repository.git 
    
    # push the local changes to the remote Git repository
    git push -u origin main
    
    ```

    This code pushes the changes \(in the local Git repository\) to the specified remote repository on the Git server.


