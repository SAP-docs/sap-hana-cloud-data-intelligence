<!-- loiod7dfd729717e419cbf8697295dd096c1 -->

# Read Data From SAP System

The `Read Data from SAP System` operator establishes a connection between your ABAP-based SAP system and SAP Data Intelligence.



You can then use the operator `Read Data from SAP System` to replicate tables, CDS views, and ODP objects from a source system into SAP Data Intelligence. Depending on the source system version and products installed, the available options are presented to you when selecting the object to be replicated. For more information about what is possible with this operator, see SAP Note [2890171](https://me.sap.com/notes/2890171).



<a name="loiod7dfd729717e419cbf8697295dd096c1__section_ukw_byw_prb"/>

## Reading Data from a Table

If you want to read data from a table, you must first create an SLT configuration in the ABAP system. To do so, run transaction code `LTRC` in the SLT system and specify the scenario type as `SAP Data Intelligence (Generation 2 Operators)`.

> ### Note:  
> You can find more information about replicating data to SAP Data Intelligence on the SAP Help Portal. On the [SAP LT Replication Server landing page](https://help.sap.com/sapslt) under Getting Started, you can open the SAP Help Portal documentation by selecting the link SAP Landscape Transformation Replication Server. Select the node `Replicating Data to SAP Data Intelligence`.

The information that you need later \(when using the operator\) is the mass transfer ID that is automatically assigned to your configuration: You have to specify it together with the table name and connection information.

When you then run the related graph, the table is automatically assigned to the mass transfer ID you defined previously. If you chose the transfer mode `Replication`, the system automatically switches to the transfer of delta data once the initial load is completed. In the delta phase, the system not only replicates the changes made in the source, but also provides information about what operation took place for each relevant data record \(such as "update" or "delete"\).

When you stop or pause the graph, the operator `Read Data from SAP System` triggers a `Suspend` action in the SLT system, and the replication of the table is suspended automatically. When you archive or delete the graph after stopping it, the operator `Read Data from SAP System` triggers the corresponding `Stop` action in the SLT system, and the replication of the table is stopped automatically.



<a name="loiod7dfd729717e419cbf8697295dd096c1__section_ely_wyw_prb"/>

## Reading Data from a CDS View

The CDS view you want to read data from must be enabled for data extraction. You can use the CDS view`I_DataExtractionEnabledView` to check if the actions *Initial Load*, *Replication*, and *Delta Load* are possible for a CDS view.



<a name="loiod7dfd729717e419cbf8697295dd096c1__section_a1b_lm1_gvb"/>

## Reading Data from an ODP Object

The ODP objects you want to read data from must be created in the SAP source system and available in the SAP Data Intelligence object browser. Replicating data from ODP SAPI extractor objects using transfer modes `Replication` or `Delta Load` is only possible if the relevant objects support real-time replication, and the source has a timestamp or numeric \(unique sequential number\) field. Please refer to the ODP help for further details about ODP object creation.

The following object types are supported:

-   Extractors \(using context SAPI\) and DataStore objects
-   CompositeProviders \(Object type HCPR\)
-   InfoCubes
-   Semantically Partitioned Objects
-   HybridProviders
-   MutiProvidersInfoSets
-   InfoObjects for master data, texts, and hierarchies
-   Queries as InfoProviders \(using context BW\)



## Authorizations

The user specified in the ABAP connection needs authorizations for the operator and the data that is selected. For details, see the information about user authorizations in SAP Note [3100673](https://me.sap.com/notes/3100673).



<a name="loiod7dfd729717e419cbf8697295dd096c1__section_omz_hzw_prb"/>

## Resilience

By default, this operator uses the snapshot feature, which is a necessary prerequisite for operator resilience. When running a graph that includes this operator, you can choose whether you want to enable the option for capturing snapshots using either the *Run As* or the *Schedule* option.

Deactivating the snapshot feature may make sense if you want to use the operator in a graph together with operators that do not support it. \(All operators in a graph must either support or not support the snapshot feature.\) However, if you deactivate the snapshot feature, the resilience features are not available for this operator either. Consider the pros and cons for your specific use case before deactivating the snapshot feature.



<a name="loiod7dfd729717e419cbf8697295dd096c1__section_rtb_tzw_prb"/>

## Configuration Parameters

-   **ABAP Connection**: The connection information for the ABAP-based remote system. You can select a predefined ABAP connection from the Connection Manager.
-   **Object Name**:

    To specify a **table**, ensure that a suitable mass transfer ID exists in the SLT system. Then, proceed as follows:

    1.  Choose the *Browse* button next to the *Object Name* field. The system displays the *Object Name* popup where you can search for the relevant table.
    2.  Double-click *SLT*.
    3.  The system displays a list of the mass transfer IDs that are available in the connected system.
    4.  Double-click the relevant mass transfer ID.
    5.  Enter the table name in the *Search* field.
    6.  Select the relevant table and choose the OK button. The system fills the *Object Name* field with the relevant information for the table.

    To specify a **CDS view**, proceed as follows:

    1.  Choose the *Browse* button next to the *Object Name* field.
    2.  Double-click *CDS\_EXTRACTION* to get a list of the CDS views that are enabled for extraction.

        > ### Note:  
        > Depending on the type and release level of your source system, CDS\_EXTRACTION may not be available. If this is the case for you, double-click CDS instead and drill down to the relevant CDS views as explained in step 3 below.

    3.  \(optional – only relevant for CDS, **not** for CDS\_EXTRACTION\): The system displays a list of application components. A CDS view belongs to a package, and the package belongs to an application component. You need to first navigate to the relevant application component. Example: You want to load the CDS view `I_CalendarDate`, which belongs to application component `CA-GTF-DF`. The system displays the first part of the application component, `CA`. You need to navigate to the relevant application component by double-clicking on `CA` and then `GTF` and so on.

        If you only know the name of the CDS view, but not its application component, you can search for the CDS view. The system will show the first part of the correct application component, for example CA. Double-click CA, then search again with the CDS view name. The system will show the second part of the correct application component, for example GTF and so on.

    4.  The system displays the CDS views that belong to the relevant component.
    5.  Select the relevant CDS view and choose the *OK* button. The system fills the *Object Name* field with the relevant information for the CDS view.

    To specify an ODP object, proceed as follows:

    1.  Choose the *Browse* button next to the *Object Name* field. The system displays the *Object Name* popup where you can search for the relevant ODP object.
    2.  Double-click *ODP\_SAPI* \(for extractors\) or *ODP\_BW* \(for all other supported objects\).
    3.  The system displays a list of nodes. Navigate to the relevant node.
    4.  The system displays the objects that belong to the relevant node.
    5.  Select the relevant ODP object and choose the *OK* button. The system fills the *Object Name* field with the relevant information for the ODP object.

-   *Transfer Mode*: Can have one of the following values:
    -   *Initial Load*: Copy all relevant data from the source to the target \(once\).
    -   *Delta Load*: Whenever data gets changed \(for example, added or deleted\) in the source, copy these changes immediately from the source to the target \(ongoing\).
    -   *Replication*: Do initial load followed by delta load.




<a name="loiod7dfd729717e419cbf8697295dd096c1__section_ngg_qbx_prb"/>

## Input

None



<a name="loiod7dfd729717e419cbf8697295dd096c1__section_ilm_sbx_prb"/>

## Output

`outData`: Output the source data; type: `table`

The data structure of the output data type depends on the type of the object that is being read. It is extended by an additional field that specifies the operation. You can find the name of the field specifying the operation in component `changeModeColumnName` in the CDC header \(see below for details\).

The possible parameter values for operations in the source system are different from the possible values in SAP Data Intelligence. To accommodate for this, the values from the source system are mapped to the corresponding values in SAP Data Intelligence as described below.

-   Body header `com.sap.headers.body` with the following components:
    -   `id`: vtype ID for output
    -   `type`: table
    -   `size`: transferred data volume \(in bytes\)
    -   `schema`: is always empty

-   Batch header `com.sap.headers.batch` with the following components:
    -   `index`: package number of current data package if transfer mode = ‘Initial Load’; ‘0’ if transfer mode is different from ‘Initial Load'
    -   `isLast`: always ‘true’ for transfer modes Delta Load and Replication; for Initial Load, ‘false’ for all packages except the last one and 'true' for the last package; for more information, see SAP Note [3198623](https://me.sap.com/notes/3198623)
    -   `count`: ‘0’ if transfer mode is ‘Initial Load’; ‘1’ if transfer mode is different from ‘Initial Load’
    -   `size`: maximum possible size of a data package in bytes \(intended size\)
    -   `unit`: bytes

-   CDC header `com.sap.headers.cdc` with the following components:

    SAP S/4HANA source system

    -   `changeModeColumnName`: `/1DH/OPERATION`
    -   `sequenceNumberColumnName`: empty

-   DMIS source system

    -   `changeModeColumnName`: `IUUC_OPERATION`
    -   `sequenceNumberColumnName`: empty

    The values in the `changeModeColumnName` column indicate which operation was executed on the record in the source table. The values from the source system are mapped to the corresponding values in SAP Data Intelligence as outlined in the table below:


    <table>
    <tr>
    <th valign="top">

    Operation Type
    
    </th>
    <th valign="top">

    ABAP
    
    </th>
    <th valign="top">

    SAP Data Intelligence
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Insert
    
    </td>
    <td valign="top">
    
    'I'
    
    </td>
    <td valign="top">
    
    'I'
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Initial Load
    
    </td>
    <td valign="top">
    
    ' '
    
    </td>
    <td valign="top">
    
    'L'
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Update
    
    </td>
    <td valign="top">
    
    'U'
    
    </td>
    <td valign="top">
    
    'A'
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Delete
    
    </td>
    <td valign="top">
    
    'D'
    
    </td>
    <td valign="top">
    
    'X'
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Archive
    
    </td>
    <td valign="top">
    
    'A'
    
    </td>
    <td valign="top">
    
    'M'
    
    </td>
    </tr>
    </table>
    
    The mapping assigns the correct value in SAP Data Intelligence to each value from the source system. For more information, see SAP Note [3241904](https://me.sap.com/notes/3241904).


