<!-- loio991a6dc7269a43c78185cdcfe6fb4f56 -->

# Create Tasks

In a replication flow, a task is an executable component that consists of a source dataset, its corresponding target, and any associated configuration options such as filters, mappings, and load type.



## Context

A replication flow must contain at least one task.

When you create a task, the target dataset name matches that of the source dataset, but you can change it.

During execution, the system checks if the target dataset exists. For a database, the target dataset is a table; for object stores and data lakes, the target dataset is a folder or set of files with the same prefix. If the target dataset does not exist, the system creates the table or folder, respectively.

> ### Note:  
> If you add a new name for an object store target, do not use the characters dot \(.\) or forward slash \(/\) in the name.



## Procedure

1.  Choose the *Tasks* tab.

2.  Choose *Create*.

    The *Add Datasets* dialog displays.

3.  In the *Add Datasets* dialog, navigate through the folder hierarchy, if necessary, or add a dataset name in the search box \(required for SLT sources\). Choose one or more datasets from the list and choose *OK*.

    Note that a given source dataset can't be used in more than one replication flow.

4.  Add filters and custom mappings to the task.

5.  To change the target to an existing object \(table or folder\), in the *Target* column, choose the *Select Target* icon next to the target name and browse to the object. It is also possible to manually add a new target name. The name is limited to 64 characters.

    > ### Note:  
    > When you change the target of an object store by choosing an existing folder, the folder must be empty; if not, you must choose the *Truncate* option to enable task execution.

6.  The default *Load Type* is *Initial Only*. To enable delta loading for this task, choose *Initial and Delta*.

7.  To clear the content of the target before the task runs, choose *Truncate*.

8.  Save the replication flow.




## Next Steps

You can now validate the replication flow to ensure it's ready to deploy and run.

-   **[Add a Filter](add-a-filter-7df99cc.md "For a given task, you can optionally add one or more filters to a dataset to customize
		the target. ")**  
For a given task, you can optionally add one or more filters to a dataset to customize the target.
-   **[Define the Mapping for a Dataset](define-the-mapping-for-a-dataset-6c0ed1f.md "For existing target tables, you can edit the mapping of a dataset to customize it. Or, for a target table that doesn't exist yet, SAP Data Intelligence replication flow lets you define the table by specifying column names and
		data-type information. ")**  
For existing target tables, you can edit the mapping of a dataset to customize it. Or, for a target table that doesn't exist yet, SAP Data Intelligence replication flow lets you define the table by specifying column names and data-type information.
-   **[Data Type Compatibility](data-type-compatibility-e81bd11.md "SAP Data Intelligence replication flow maintains data type compatibility between source and
		target data types.")**  
SAP Data Intelligence replication flow maintains data type compatibility between source and target data types.

**Related Information**  


[Validate the Replication Flow](validate-the-replication-flow-c716063.md "Validation ensures the minimum requirements have been specified for the replication flow for deployment and execution.")

