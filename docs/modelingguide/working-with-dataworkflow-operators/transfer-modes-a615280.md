<!-- loioa6152803801f49d8b730088a77c5f05d -->

# Transfer Modes

The Data Transfer operator in SAP Data Intelligence supports different modes for retrieving data.

Use the Data Transfer operator to retrieve data using any of the following modes:

-   SAP Business Warehouse \(BW\) OLAP. \(Use the OLAP Interface \(INA\) protocol as the access method.\)
-   Generated SAP HANA views.
-   SAP BW ODP for full or delta data extraction.

For all other cases, the preferred way is to use SAP HANA. To use SAP HANA, mark a specific query, infoprovider, or datastore in the query designer to generate an underlying calculation view. SAP Data Intelligence queries this view to transfer the data to other target systems.

> ### Note:  
> The application processes the partition result sets one after the other and not in parallel.



<a name="loioa6152803801f49d8b730088a77c5f05d__section_tnd_g2t_gjb"/>

## SAP BW OLAP

SAP BW OLAP is the default mode. SAP BW uses OLAP to access data. The OLAP method ensures that the data you write matches the data from the common SAP BW user interfaces, such as Transaction RSRT2. The OLAP method supports a wide variety of SAP BW functionality.

Because of the online nature of the OLAP access method, SAP doesn't recommend it for large-scale data transfer. With the SAP BW OLAP mode, transfer the complete data in a single result set.

> ### Note:  
> SAP BW INA has a maximum number of cells that can be exported.



<a name="loioa6152803801f49d8b730088a77c5f05d__section_pff_g2t_gjb"/>

## Generated SAP HANA Views

Generate designated calculation views on the underlying SAP HANA database for each query or infoprovider in SAP BW on SAP HANA and SAP BW/4HANA. SAP Data Intelligence uses generated SAP HANA views when the following condition are met:

-   You create a connection to an SAP BW system using the SAP Data Intelligence Connection Management application.
-   You use SAP BW version 4.2.0 and higher.
-   You specify a working connection to the SAP HANA database and referenced it in the SAP BW connection that you use.
-   You upload two certificates for SSL access in case the two connections can't be covered by the same root certificate.
-   You ensure that the corresponding query or infoprovider has a generated calculation view.
-   The projection of chosen dimensions and measures doesn't contain a restricted attribute, such as specified in [2145502](https://me.sap.com/notes/2145502).
-   There are no further errors that occur, such as SAP HANA authorization errors.

If data is retrieved with generated SAP HANA views, then you can specify partitions of data. The application transfers partitions of data separately, which enables large result sets.



<a name="loioa6152803801f49d8b730088a77c5f05d__section_rvg_g2t_gjb"/>

## SAP BW ODP

You can use the SAP BW ODP mode only with datastores.

> ### Note:  
> You must change the setting in the Data Transfer operator manually to activate querying with SAP HANA. The application uses the non-optimised BW INA provider for data extraction in the following cases:
> 
> -   If SAP HANA isn't available.
> -   If the application doesn't generate the necessary calculation view.
> -   If you've selected the INA option explicitly.
> 
> If the application uses the non-optimised BW INA provider, it requires that you provide an appropriate timeout for the BW INA call, depending on the amount of data you expect to be extracted.

In the current version, SAP Data Intelligence supports the following file storage targets for data transfer using the SAP BW ODP mode:

-   ADL \(Microsoft Azure Data Lake\)
-   GCS \(Google Cloud Storage\)
-   HDFS \(Hadoop Distributed File System\)
-   OSS \(Alibaba Cloud Object Storage Service\)
-   S3 \(Amazon Simple Storage Service\)
-   SDL \(Semantic Data Lake\)
-   WASB \(Microsoft Azure Storage Blob\)

