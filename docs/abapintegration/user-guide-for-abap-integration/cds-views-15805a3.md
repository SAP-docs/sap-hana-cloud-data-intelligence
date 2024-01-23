<!-- loio15805a351d6a4d0396071b8973dbdedc -->

# CDS Views

What you need to do to integrate data using ABAP CDS views depends on whether you want to use SAP S/4HANA or SAP S/4HANA Cloud as the data source.

For *SAP S/4HANA Cloud*, you have the following options:

-   You can integrate data from standard ABAP CDS views that have the required annotations as part of the C1 release contract.

-   You can create custom CDS Views to integrate data with SAP Data Intelligence Cloud. For more information, see [Custom CDS Views](https://help.sap.com/docs/SAP_S4HANA_CLOUD/0f69f8fb28ac4bf48d2b57b9637e81fa/e30de6eae4d24d70b65996ac8ff88848.html?version=2302.502&q=custom%20cds%20views).


For *SAP S/4HANA*, you have the following options:

-   You can integrate data from standard ABAP CDS views that have the required annotations as part of the C1 release contract \(in a similar way as with SAP S/4HANA Cloud\).

-   In addition, you can create custom ABAP CDS views to integrate data with SAP Data Intelligence Cloud using the ABAP Development Tool \(ADT Tool\) as described in [Loading and Replicating Data from ABAP CDS Views in SAP S/4HANA](loading-and-replicating-data-from-abap-cds-views-in-sap-s-4hana-55b2a17.md).


For more information, see also [CDS Views](https://help.sap.com/docs/SAP_S4HANA_CLOUD/0f69f8fb28ac4bf48d2b57b9637e81fa/5418de55938d1d22e10000000a44147b.html?version=2208.500).

To find out which extraction-enabled CDS views are C1-released and delta-enabled, you can use the public CDS View `I_DataExtractionEnabledView`, which is available in SAP S/4HANA Cloud as well as in SAP S/4 HANA \(as of SAP S/4HANA 2020\).

Alternatively, you can check for the following properties in the Metadata Explorer of SAP Data Intelligence Cloud:

-   Property name “Extraction Enabled” for general extraction of a specific ABAP CDS view

-   Property name “Delta enabled” for delta extraction of a specific ABAP CDS view

-   Property name “CDS Type” for checking the contract status, e.g. “C1” for C1 released ABAP CDS views


-   **[Loading and Replicating Data from ABAP CDS Views in SAP S/4HANA](loading-and-replicating-data-from-abap-cds-views-in-sap-s-4hana-55b2a17.md "To make the data from an ABAP CDS view available in SAP Data Intelligence Cloud, you need to specify specific annotations
		for the view in the ABAP Development Tool (ADT Tool).")**  
To make the data from an ABAP CDS view available inSAP Data Intelligence Cloud, you need to specify specific annotations for the view in the ABAP Development Tool \(ADT Tool\).

