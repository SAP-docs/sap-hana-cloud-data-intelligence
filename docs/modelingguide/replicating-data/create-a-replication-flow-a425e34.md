<!-- loioa425e3426b644b1184207d291a856119 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Create a Replication Flow

The SAP Data Intelligence Modeler includes an interface for creating and running replication flows.



<a name="loioa425e3426b644b1184207d291a856119__prereq_kcf_xyt_xqb"/>

## Prerequisites

Before you perform the following steps, ensure that the required source and target connections are created and enabled for you in SAP Data Intelligence Connection Management.

For delta loading tasks in a Microsoft Azure SQL database source, the source must include a schema that has the same name as the user name specified for the corresponding AZURE\_SQL\_DB connection. If this schema doesn't exist, a database administrator must create it including the necessary write privileges. This schema is required for storing internal objects for delta replication.



## Procedure

1.  Start the SAP Data Intelligence Modeler.

2.  Open the *Replications* tab in the navigation pane.

    > ### Restriction:  
    > Even though the *Schedule* tab appears in the lower panel, scheduling isn't supported in *Replications*.

3.  Select :heavy_plus_sign: in the Navigation pane menu toolbar.

4.  Enter a name for the replication flow and select *OK*.

5.  **Optional:** Add a description in the *Properties* tab.

6.  Choose a source in Source section of the *Properties* tab by performing the following substeps:

    1.  Choose a source connection from the *Source Connection* list.

        The list is sorted alphabetically. Only connections for which you have authorization are available.

    2.  Add a name or browse for the parent object that contains one or more datasets to replicate in *Container*.

        -   To replicate a database table, choose the schema that includes the table.
        -   For SAP ECC/SLT sources, browse for and open the SLT folder and choose an SLT configuration.
        -   For CDS views, browse for and select the CDS root folder.


7.  Repeat the connection and container steps for one or more of the following targets:

    > ### Note:  
    > For cloud storage, the container name is limited to 64 characters. For Kafka, there is no character limit.

    -   Amazon Web Service Storage Services \(S3\)
    -   Microsoft Azure Data Lake Storage Gen2 \(ADL\_V2\)
    -   Google Cloud Service \(GCS\)
    -   SAP HANA Data Lake \(HDL\)
    -   Kafka

8.  Complete the options as described in the following table for a cloud storage target.


    <table>
    <tr>
    <th valign="top">

    Option
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    **Group Delta By**
    
    </td>
    <td valign="top">
    
    Specifies whether you want to create additional folders for sorting updates based on the date or hour.

    For Load Type of Initial and Delta, choose one of the following options:

    -   *None*
    -   *Date*
    -   *Hour*


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **File Type**
    
    </td>
    <td valign="top">
    
    For CSV:

    -   *File Delimiter*: Specifies the character to use as a delimiter for columns in CSV files.
    -   *File Header*: Specifies whether CSV files include a header row with the column names.

    For Parquet:

    -   *File Compression*: Specifies the compression algorithm to use for Parquet files. Applicable algorithms include the following:
        -   *None*
        -   *GZIP*
        -   *Snappy*

    -   *Compatibility Mode*: Specifies a compatibility mode to use when replicating to object stores in Parquet. Options include the following:
        -   *None*: Uses the default compatible data type when you create a replication flow. For more information, see [Data Type Compatibility](data-type-compatibility-e81bd11.md).
        -   *Spark*: Converts and stores time data type columns to int64 in the Parquet files. The int64 data type represents microseconds after midnight. This conversion allows the columns to be consumed by Spark.


    For JSON:

    -   *Encoding*: Generated JSON files are encoded in UTF-8 format.

    -   *Orient*: Specifies the internal structure of the produced JSON files. Internal structures include the following:
        -   “records”: `[{column -> value}, ... ,{column -> value}]`
        -   “values”: `[value, ... ,value]`


    For jsonlines:

    *Encoding*: Generated JSON Lines files are encoded in UTF-8 format.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Suppress Duplicates**
    
    </td>
    <td valign="top">
    
    Options include the following:

    -   *True*: Minimizes the occurrence of duplicates during the initial load.
        -   If necessary for replications from ABAP, apply SAP Note [3302718](https://me.sap.com/notes/3302718) to the ABAP system.
        -   SAP Data Intelligence minimizes duplicates by generating unique file names from the source partitions and recording only once. For more information, see [Cloud Storage Target Structure](cloud-storage-target-structure-12e0f97.md).

    -   *False*: SAP Data Intelligence can deliver duplicate change records to the target. When duplicate change records are delivered to the target, the timestamp column in the file name helps you to identify the current valid record and to ignore potential duplicated records.


    
    </td>
    </tr>
    </table>
    
9.  Complete the options as described in the following table for a Kafka storage target.


    <table>
    <tr>
    <th valign="top">

    Option
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    **Serialization Type**
    
    </td>
    <td valign="top">
    
    Choose *JSON* or *Avro*. The default is JSON.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Compression**
    
    </td>
    <td valign="top">
    
    Choose one of the following compression types:

    -   *No Compression*
    -   *GZIP*
    -   *Snappy*
    -   *LZ4*
    -   *Zstandard*


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Partitions**
    
    </td>
    <td valign="top">
    
    Specifies the number of partitions to split the topic into. The default is 1.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    **Replication Factor**
    
    </td>
    <td valign="top">
    
    Specifies how many copies of data to store across several Kafka brokers. The default is 1.

    > ### Note:  
    > Replication Factor is limited to the number of Kafka brokers.


    
    </td>
    </tr>
    </table>
    
    > ### Note:  
    > The replication flow considers messages as written successfully when the message is accepted by all in-sync replicas \(`ack=all`\).

10. Save the replication flow.




<a name="loioa425e3426b644b1184207d291a856119__postreq_g4v_5cz_gqb"/>

## Next Steps

Next, create one or more tasks in the replication flow. Tasks are the executable components that consist of a source dataset, its corresponding target, and any associated configuration options.

-   **[Create Tasks](create-tasks-991a6dc.md "In a replication flow, a task is an executable component that consists of a source dataset, its corresponding target, and any associated
		configuration options such as filters, mappings, and load type. ")**  
In a replication flow, a task is an executable component that consists of a source dataset, its corresponding target, and any associated configuration options such as filters, mappings, and load type.

**Related Information**  


[Using SAP Data Intelligence Connection Management](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/974be4fbb13a48eda16f7b061508eb59.html "SAP Data Intelligence administrators or other business users with necessary privileges can use the SAP Data Intelligence Connection Management application to create and maintain connections. A connection represents an access point to a remote system or a remote data source.") :arrow_upper_right:

[Replication Flow Connections](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/f4327d3e2f7146a19e76924f8a79454a.html "The following tables list the data source and target systems supported by the replication management service in SAP Data Intelligence. This service manages the replication functionality (replication flows) in the SAP Data Intelligence Modeler application.") :arrow_upper_right:

