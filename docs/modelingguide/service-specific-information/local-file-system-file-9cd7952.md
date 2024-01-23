<!-- loio9cd7952d24f648d8babedda94a0a36af -->

# Local File System \(/file\)

Many of the SAP Data Intelligence storage operators offer support for the local file system.

The local file system is subject to the cluster's file system. The `/files/` folder seen in the System Management application can be accessed through the `/vrep/` path. For example: `/files/myfile.txt` becomes `/vrep/myfile.txt`.



<a name="loio9cd7952d24f648d8babedda94a0a36af__section_epz_xph_sfb"/>

## Restrictions

-   **/vrep is deprecated:** The usage of the `/vrep` folder in graphs is deprecated. The `/vrep` path is not meant to be used for writing and reading files. If your graphs and operators need temporary storage, consider using the `/vrep` connection type only to access a folder local to the graph container. If you need to share files between subengines or groups, consider using blob storage such as S3.
-   **Temporary files:** Operators can write files to the `/tmp` folder, which is a folder local to the graph container. However, `/tmp` is not a shared folder, so when working with groups and subengines it can't be used for file sharing.
-   **Working directory:** For any path that is given to or by this service, the current working directory \(`.`\) will be the HOME directory of the user running the local graph container. The HOME directory is `/home/vflow/` in the base docker image. You can't access other directories using absolute paths \(`..`\) to access the parent directory, because the user `/vflow` doesn't have the necessary permission.
-   **Copy file:** Because the local file system API doesn't support the `copy` operation, you must copy files using `Read + Write`.

