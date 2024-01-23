<!-- loio12e0f97395424df4a60561c2347a3b22 -->

# Cloud Storage Target Structure

Running a replication flow with a cloud storage target creates various files and structures.

For Amazon Web Service Storage Service \(S3\), Microsoft Azure Data Lake Storage Gen2 \(ADL\_V2\), Google Cloud Service \(GCS\), and HANA Data Lake \(HDL\), the replication flow proceeds as follows:

-   When the initial load completes, the system writes a `_SUCCESS` file.
-   Downstream applications that have direct access to the object store can use the `_SUCCESS` file to verify that the replication completed successfully without checking the replication flow status.

The `.sap.partfile.metadata` objects include dataset metadata information. The objects exist in the root of each data file directory and are created and referenced as part of replication flow processing. Additionally, you can leverage these objects for interpreting and processing the dataset data files.

You can view the `.sap.partfile.metadata` objects in the Metadata Explorer as follows:

```
/<container-base-path>/
    .sap.rms.container
    <tableName>/
        .sap.partfile.metadata
        initial/				  
            .sap.partfile.metadata
            part-<unix_timestamp>-<workOrderID-1>-<deliminationNo-01>.<extension>
            ...
            part-<unix_timestamp>-<workOrderID-M>-<deliminationNo-N>.<extension>
            _SUCCESS
        delta/ (only there in case of delta load)
            <date(time)-optional>/
                .sap.partfile.metadata
                part-<unix_timestamp>-<workOrderID-X>-<deliminationNo-01.<extension>
                ...
                part-<unix_timestamp>-<workOrderID-Y>-<deliminationNo-01>.<extension>
```

> ### Example:  
> > ### Sample Code:  
> > ```
> > /path/
> >    to/
> >     container1/
> >         .sap.rms.container
> >         table1.csv/
> >             .sap.partfile.metadata
> >             initial/						  
> >                 .sap.partfile.metadata
> >                 part-1634738166-a2480cda-2a7f-11ec-8d3d-0242ac130003-01.csv
> >                 part-1634738167-a2480cda-2a7f-11ec-8d3d-0242ac130003-02.csv
> >                 part-1634738169-acfe5bca-8086-4f04-9014-c1b92106cb23-01.csv
> >                 part-1634738170-b89722fa-9ff5-43e9-abdf-3d73827447cb-01.csv
> >                 _SUCCESS
> >             delta/
> >                 .sap.partfile.metadata
> >                 20211020/
> >                     .sap.partfile.metadata
> >                     part-1634738180-cde25008-53e2-4b41-949e-b992f4f0f04d-01.csv
> >                     part-1634739123-d60a2652-2801-4db4-8d7b-f20a6b09ef87-01.csv
> >                 20211021/
> >                      .sap.partfile.metadata
> >                     part-1634824512-f2c188d0-2a7f-11ec-8d3d-0242ac130003-01.csv
> >         table2.csv/
> >            .sap.partfile.metadata
> >            initial/
> >                .sap.partfile.metadata
> >                part-1634738166-2bac0984-3888-11ec-8d3d-0242ac130003-01.csv
> >                ... 
> >     container2/
> >         table2.parquet/								  
> >             .sap.partfile.metadata
> >             initial/
> >                 .sap.partfile.metadata 
> >                 part-1634738166-db1a8efa-3887-11ec-8d3d-0242ac130003-01.parquet
> >                 part-1634738167-db1a8efa-3887-11ec-8d3d-0242ac130003-02.parquet
> >                 ...
> > ```

If you set *Suppress Duplicates* to *true*, the file names in the `initial` folder contain an internal-id consisting of 33 base64URL characters.

The target structure may look like the following:

```
/<container-base-path>/
    .sap.rms.container
    <tableName>/
        .sap.partfile.metadata
        initial/				  
            .sap.partfile.metadata
            part-<internal-id>.<extension>
             ...
            part-<internal-id>.<extension>
            _SUCCESS
        delta/ (only there in case of delta load)
            <date(time)-optional>/
                .sap.partfile.metadata
                part-<unix_timestamp>-<workOrderID-X>-<deliminationNo-Y>.<extension>
                ...
                part-<unix_timestamp>-<workOrderID-Y>-<deliminationNo-Y>.<extension>
```

The replication flow creates multiple dataset files \(<code>part-*.<i class="varname">&lt;extension&gt;</i></code>\) during initial and delta loading. The number and size of the dataset files depends on the following factors:

-   Source table size.
-   Source table structure.
-   Change frequency during delta loading.

Each dataset file contains the source columns. Source columns are defined in the dataset mapping in the replication flow task. In addition, the system appends the column as described in the following table.


<table>
<tr>
<th valign="top">

Column Name

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`__operation_type`

</td>
<td valign="top">

Identifies the type of target row. The possible values are as follows:

-   *L*: Written as part of the initial load.

-   *I*: After the initial load completed, new source row added.

-   *U*: After the initial load completed, after image of an update to a source row.

    > ### Note:  
    > For some sources the system switches the value *U* to *A* after you apply SAP Note [3044005](https://me.sap.com/notes/3044005). The APE\_KEEP\_UPDATE\_OPERATION parameter is described in the SAP Note.

-   *B*: After the initial load completed, before image of an update to a source row. These records are only sent by some sources \(like SAP HANA\) and only when the after image of the update is not passing the filters specified in the replication task.

-   *X*: After the initial load completed, source row deleted. The only target columns to contain data for this operation code are codes that reflect the source key columns. All other target columns are empty.

-   *M*: After the initial load completed, archiving operations.




</td>
</tr>
<tr>
<td valign="top">

`__sequence_number`

</td>
<td valign="top">

An integer value that reflects the sequential order of the delta row in relation to other deltas. This column is empty for initial load rows and isn't populated for all source systems \(for example, ABAP\).

</td>
</tr>
<tr>
<td valign="top">

`__timestamp`

</td>
<td valign="top">

The UTC date and time the system wrote the row.

</td>
</tr>
</table>

