<!-- loio657daa0141d54e4793ed9f95c695fd39 -->

# ODP

To extract data using ODP, SAP Data Intelligence Cloud connects directly to the SAP system that acts as the data source.



The following prerequisites apply:

-   If you want to work with generation 1 operators, you need the DMIS add-on as well as version 2 of the ODP Application API.

-   If you want to work with replication flows or generation 2 operators using an SAP S/4HANA system as the source, you only need the ODP Application API. For older source systems, you need the DMIS add-on and the ODP Application API.

-   You have considered the ODP-related information and recommendations in the most recent version of SAP Note [2890171](https://me.sap.com/notes/2890171).

-   The prerequisites for ODP integration with SAP Data Intelligence Cloud \(as described in SAP Note [2775549](https://me.sap.com/notes/2775549)\) are fulfilled.

-   The technical user for using the ODP interface has the required privileges assigned. For more information, see SAP Note [3100673](https://me.sap.com/notes/3100673).


The recommended connection type for working with ODP data is [ABAP](https://help.sap.com/docs/SAP_DATA_INTELLIGENCE/ca509b7635484070a655738be408da63/612f8de3696647c5a16e9c7d1fb4d778.html?version=Cloud). If you cannot use this connection type \(for example because you cannot install the DMIS add-on in the source system\), you can use [ABAP\_LEGACY](https://help.sap.com/docs/SAP_DATA_INTELLIGENCE/ca509b7635484070a655738be408da63/fe9c391730d4456895340ed24e3cad7b.html?version=Cloud). ABAP\_LEGACY only requires ODP Application API version 2.0 \(and neither the DMIS add-on nor the ABAP Pipeline Engine\), but does not include the latest features that are available with connection type ABAP, such as resilience and replication flows.

