<!-- loio6a74c61b826f4faba84218dbf58f8b2d -->

# Using the Data Browser Extension

The Data Browser extension in JupyterLab allows you to access datasets stored in the Metadata Explorer and connections defined in the Connection Management app.



<a name="loio6a74c61b826f4faba84218dbf58f8b2d__prereq_lwc_z3k_rlb"/>

## Prerequisites

You need the following user policies to use the Data Browser extension:

-   `sap.dh.member` – Provides access to the tenant

-   `sap.dh.metadata` – Lets you view the files and folders in the data collection along with the metadata

    > ### Note:  
    > `sap.dh.metadata` is deprecated and will be removed in future releases. Instead, you can use `app.datahub-app-data.fullAccess` as a close replacement.

-   `sap.dh.developer` – Lets you copy data to the clipboard to create a pipeline




<a name="loio6a74c61b826f4faba84218dbf58f8b2d__context_ckd_3mq_qlb"/>

## Context

For datasets and connections, the Data Browser generates a script that you can use to create a pipeline and copy data from a data source connection to the data lake. This means that you don't have to authenticate yourself to use the connections. For workspaces and collections, the Data Browser uses the Python SDK to retrieve data and add it to a pandas dataframe.

As a data source, the following relational databases are supported:

-   DB2

-   MySQL

-   Oracle

-   SAP HANA

-   SQL Server




<a name="loio6a74c61b826f4faba84218dbf58f8b2d__steps_xvy_j4n_sjb"/>

## Procedure

1.  From the Tabs panel in the left sidebar, click *Data Browser* \(![](images/Icon_Data_Browser_34a7f4f.png)\).

2.  Select the required tab:

    -   *Metadata Catalog* lets you access datasets stored in the Metadata Explorer.
    -   *Connections* lets you access the connections as defined in the *Connection Management* app.

3.  Browse to the required item by double-clicking through the directory structure or by using the search field.

    Note that you may need to refresh the items if a dataset, connection, workspace, or data collection has recently been added. You can also branch to the item in the associated app by clicking the corresponding option in the context menu.

4.  Depending on the tab you selected, proceed in one of the following ways:

    -   For metadata and connections, click *Copy pipeline script* \(![](images/Copy_Script_dc92a7c.png)\) to generate a script and add it to your clipboard. Then paste the script into your notebook.
    -   For data workspaces and data collections, click *Copy code script* \(![](images/Copy_Script_dc92a7c.png)\) to generate the code and add it to the notebook.




<a name="loio6a74c61b826f4faba84218dbf58f8b2d__result_xg5_2tn_sjb"/>

## Results

When you run the script that was generated for metadata and connections, the pipeline is created and executed. You can monitor it using the *Modeler* app. The pipeline generates a new folder in the `/shared` directory of the data lake and the system assigns the same name as the datasets. You can modify the script as required before you run the pipeline. The generated files contain the data from the data lake, which can be consumed by the HDFS client in the Jupyter notebook.

For data workspaces and data collections, a pipeline is not generated. Instead, the workspaces and collections are accessed via the SDK.

