<!-- loio5d7d9e25afb642ed9f4b21f0c62f9871 -->

# Using Git Terminal

Use the Git terminal to integrate SAP Data Intelligence file-based content, such as graphs, operators, docker files, or script code, with an existing Git server.

Keep a version history of changes in Git and work collaboratively with other developers by sharing content files in Git.

Leverage Git capabilities in the SAP Data Intelligence Modeler application, and perform the following basic tasks:

-   Maintain Git credentials using standard Git Credential Helper.
-   Create a local Git repository.
-   Clone a remote Git repository.



<a name="loio5d7d9e25afb642ed9f4b21f0c62f9871__section_qwb_rc4_m5b"/>

## Other Git Features

In addition to the Git commands for the basic configurations, there are other one-line commands and features of the Git command-line client for Linux. For example, use the following one-line codes:

-   `git branch`: Creates a new branch.
-   `git merge`: Combines a specified branch history with the current branch.
-   `git rebase`: Change a series of commits that modify the history of your repository.
-   `.gitignore files`:

    -   Prevent tracking specific artifacts that are in both the Git repository and the working directory, such as the Modeler workspace.
    -   Manipulate the content of the `info/exclude` file in the `.git` directory of the local Git repository.

    > ### Example:  
    > To ignore all files and track only one `graph.json` file, run the following command:
    > 
    > ```
    > 
    > # setup repo to ignore everything
    > Export GIT_DIR=vhome/.git
    > echo '# ignore everything' >> $GIT_DIR/info/exclude
    > echo '*' >> $GIT_DIR/info/exclude
    > echo '# but allow directories' >> $GIT_DIR/info/exclude
    > echo '!*/' >> $GIT_DIR/info/exclude
    > echo '# add include pattern below starting with !' >> $GIT_DIR/info/exclude
    > 
    > echo '!vflow/graphs/demo-graph/**' >> $GIT_DIR/info/exclude
    > 
    > ```


-   **[Git Credential Handling Using Standard Git Credential Helper](git-credential-handling-using-standard-git-credential-helper-d5d6805.md "To avoid entering credentials for each Git command, configure either git-credential-store or
			git-credential-cache.")**  
To avoid entering credentials for each Git command, configure either `git-credential-store` or `git-credential-cache`.
-   **[Create a Local Git Repository](create-a-local-git-repository-27c6f55.md "Use the Git Terminal in the SAP Data Intelligence
		Modeler application to create a local Git repository, then push the graph to your remote Git repository location.")**  
Use the Git Terminal in the SAP Data Intelligence Modeler application to create a local Git repository, then push the graph to your remote Git repository location.
-   **[Clone a Remote Git Repository](clone-a-remote-git-repository-79cfcbf.md "")**  


