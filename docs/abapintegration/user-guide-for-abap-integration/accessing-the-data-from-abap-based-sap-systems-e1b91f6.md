<!-- loioe1b91f6479a34161a79ffb51f7e60b80 -->

# Accessing the Data from ABAP-based SAP Systems

The general process for data extraction with an ABAP-based SAP system as the source is the same as for any other data source in SAP Data Intelligence Cloud. However, there are a few specific aspects to be considered and prerequisites to be met:

-   SAP Note [2890171](https://me.sap.com/notes/2890171) is the central note for ABAP integration and contains important information, for example regarding minimum release requirements for each use case or recommendations regarding the system landscape and setup. Read the latest version of the note carefully to ensure that you have the most up-to-date information.

-   SAP Data Intelligence Cloud has its own connection type for use with ABAP-based source systems. For more information about it, see the description under [ABAP](https://help.sap.com/viewer/ca509b7635484070a655738be408da63/Cloud/en-US/612f8de3696647c5a16e9c7d1fb4d778.html) and SAP Note [2835207](https://me.sap.com/notes/2835207).

-   If you use an SAP S/4HANA system, you can extract data based on CDS views. \(This is the recommended approach.\)

    If you use an older system \(that does not have CDS views\), or if your use case requires extracting data from an SAP S/4HANA system at table level, you can alternatively extract data based on tables. In this case, you use SAP Landscape Transformation Replication Server \([SLT](https://help.sap.com/slt)\) technology to perform the data extraction, and the recommended approach is to use a dedicated SLT system.

    Another possible option for extracting data is to use ODP \(for example for business extractors\).

-   To be able to access the scenario-related SAP system functionality, you need to include the required function modules in the allow list using 'UCON' for WebSocket RFC. For a list of relevant function modules, see SAP Note [2835207](https://me.sap.com/notes/2835207).

-   If you want to use an SAP S/4HANA Cloud system as the source, consider the information about integration provided under [Data Integration](https://help.sap.com/docs/SAP_S4HANA_CLOUD/0f69f8fb28ac4bf48d2b57b9637e81fa/c3a5da91691d4ebd89748d9f40af7a4c.html?version=2202.501).


The following table gives a high-level overview of the available options:


<table>
<tr>
<th valign="top">

Source System Type

</th>
<th valign="top">

Objects That Can Be Used

</th>
</tr>
<tr>
<td valign="top">

SAP S/4HANA Cloud

</td>
<td valign="top">

CDS views

</td>
</tr>
<tr>
<td valign="top">

SAP S/4HANA

</td>
<td valign="top">

CDS views

Tables \(requires SLT\)

ODP \(using ODP\_BW and ODP SAPI context, for example to access data from business extractors\)

</td>
</tr>
<tr>
<td valign="top">

SAP Business Suite

\(such as an SAP ECC System\)

</td>
<td valign="top">

CDS views

Tables \(requires SLT\)

ODP \(using ODP\_BW and ODP SAPI context, for example to access data from business extractors\)

</td>
</tr>
<tr>
<td valign="top">

SAP Business Warehouse

</td>
<td valign="top">

CDS views

Tables \(requires SLT\)

ODP \(using ODP\_BW and ODP SAPI context, for example to access data from \(advanced\) data store objects\)

</td>
</tr>
</table>

-   **[CDS Views](cds-views-15805a3.md "What you need to do to integrate data using ABAP CDS views depends on whether you want to use SAP S/4HANA or SAP S/4HANA Cloud as the data
		source.")**  
What you need to do to integrate data using ABAP CDS views depends on whether you want to use SAP S/4HANA or SAP S/4HANA Cloud as the data source.
-   **[Tables](tables-a100788.md "To extract data directly from tables, you additionally need SAP Landscape Transformation Replication Server (SLT), which acts as an
		intermediary between your data source and SAP Data Intelligence
                                Cloud.")**  
To extract data directly from tables, you additionally need SAP Landscape Transformation Replication Server \(SLT\), which acts as an intermediary between your data source and SAP Data Intelligence Cloud.
-   **[ODP](odp-657daa0.md "To extract data using ODP, SAP Data Intelligence
                                Cloud connects directly to
		the SAP system that acts as the data source. ")**  
To extract data using ODP, SAP Data Intelligence Cloud connects directly to the SAP system that acts as the data source.
-   **[Data Type Mapping and Conversion](data-type-mapping-and-conversion-ac9a8e3.md "When extracting data from an ABAP-based source system and transferring it to a target system, it is not always possible to keep the data
		content and source format as-is (for technical reasons). Where necessary, the ABAP data types from the source are automatically replaced with
		their respective string representations during the data transfer. (This is also known as wire format conversion.)")**  
When extracting data from an ABAP-based source system and transferring it to a target system, it is not always possible to keep the data content and source format as-is \(for technical reasons\). Where necessary, the ABAP data types from the source are automatically replaced with their respective string representations during the data transfer. \(This is also known as wire format conversion.\)

