<!-- loio031d695fda79405f8ffc88d085a48c1d -->

# Saving Diagnostic Information for Graphs on External Storage

Save a zipped archive of information for your graphs on external storage to help diagnose issues.

The SAP Data Intelligence Modeler allows saving diagnostic information for graphs on external storage. It saves the archive for graphs that reach the final state, depending on the configured System Management properties for the tenant.

-   Set the property *Enable diagnostics archive to external storage defined via Connection ID* to `true` to enable the feature.

-   Specify the Connection ID for the storage expected to be used on the property *Connection ID for diagnostics storage*. It supports the HDFS, WebHDFS, S3, ADL, GCS, SFTP, OSS, HDL, WASB, and SDL connection types.
-   Set the property *Store diagnostics on external storage only for failed graphs* to `true` when it should store diagnostics for failed graphs exclusively. Otherwise, to store the diagnostic archive to any final graph, this property should be `false`.
-   Specific graph: In the *Status* tab, select Download Diagnostic Information next to a graph to generate a zip archive of information about the graph and its subgraphs.
-   The property *Garbage collector strategy for diagnostics storage* allows to choose wheather the graph archive should never be removed from the storage or wheather it should be removed when historical graphs are removed. If the `history` option is chosen, the files are removed according to the graph garbage collector parameter `Execution history retention time limit`.
-   Data on the storage defined always follows a path pattern: `<rootPath-from-connection>/graph_diagnostics/<tenant>/<user>/graph_<handle>.zip`, where [Diagnostic Information Archive Structure and Contents](diagnostic-information-archive-structure-and-contents-a49ed7b.md) is the directory structure and contents of the diagnostic information archive.



<a name="loio031d695fda79405f8ffc88d085a48c1d__section_tly_xk5_gxb"/>

## Current Limitations

-   If one of the Modeler applications is being downscaled in parallel when a graph reaches its final state, the graph diagnostics archive may not be stored.
-   The object store is not automatically cleaned up when a user or tenant is deleted.
-   If the underlying storage or connection changes after enabling the feature, the previous storage is not automatically cleaned up.
-   Custom time-based cleanup of the stored archives is not supported.

