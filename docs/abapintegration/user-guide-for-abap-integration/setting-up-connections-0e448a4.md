<!-- loio0e448a44d54c4782b5ed35ec31031244 -->

# Setting Up Connections

For establishing the connection between your source system and SAP Data Intelligence Cloud, you can use either Remote Function Call \(RFC\) or WebSocket RFC.



The process for setting up a connection is always the same, irrespective of whether you use SAP Landscape Transformation Replication Server \(SLT\), an SAP S4/HANA system, or an SAP Business Warehouse \(SAP BW\) system. When setting up the connection, consider the following:



<a name="loio0e448a44d54c4782b5ed35ec31031244__section_y2k_ttn_psb"/>

## RFC

-   Create or reuse a communication or dialog user that has the necessary authorizations for accessing application tables in the SAP system as well as the necessary connectivity privileges in SAP Data Intelligence Cloud. For more information, see [Security Information](security-information-0192869.md).

-   Consider the security-related information that is provided with your version of SAP Data Intelligence Cloud.

-   Use the connection management in SAP Data Intelligence Cloud to establish a connection to the source SAP system. If possible, establish a naming convention for the connection names, for example SID\_MANDT\_PROTOCOL \(so that a connection would be called, for example, P25\_001\_RFC\). Secure Network Communication \(SNC\) is available as an option.




<a name="loio0e448a44d54c4782b5ed35ec31031244__section_pdm_d5n_psb"/>

## WebSocket RFC

In addition to the prerequisites described for RFC above, the following prerequisites must be met:

-   Make sure that the corresponding service infrastructure is set up correctly.

-   Make a note of the configured port \(which is usually the HTTPS port, see transaction SMICM in your source SAP system\).

-   `rfc/websocket/external_active` must be enabled to allow external RFC over WebSocket RFC.

-   To ensure that only allowed function modules can be used \(which is recommended\), activate UCON for WebSocket RFC \(ucon/websocketrfc/active\) and include the relevant function modules in the UCON allowlist. For more information, see [Security Information](security-information-0192869.md).




<a name="loio0e448a44d54c4782b5ed35ec31031244__section_ftl_35n_psb"/>

## Further Considerations

-   Make sure that an ALIAS has been defined for the relevant user name, and this ALIAS has been entered as a user in the connection management in SAP Data Intelligence Cloud .
-   If you want to extract data from an ABAP-based on-premise SAP system into SAP Data Intelligence Cloud, you need to use [Cloud Connector](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e6c7616abb5710148cfcf3e75d96d596.html#loioe6c7616abb5710148cfcf3e75d96d596__context) \(SCC\).
-   If you want to use an ABAP CDS pipeline in SAP Data Intelligence Cloud to subscribe to public CDS views from an SAP S/4HANA Cloud system and consume data from these views, you need to use the integration scenario [SAP\_COM\_0532](https://help.sap.com/viewer/0f69f8fb28ac4bf48d2b57b9637e81fa/2202.500/en-US/f509eddda867452db9631dae1ae442a3.html?q=SAP_COM_0532).

-   If you want to work with metadata from an ABAP-based SAP system, you need to use the integration scenario [SAP\_COM\_0576](https://help.sap.com/docs/SAP_S4HANA_CLOUD/0f69f8fb28ac4bf48d2b57b9637e81fa/beaebe2b20c645ce82d9490209f821a7.html).


-   **[Establishing a Connection Using Cloud Connector](establishing-a-connection-using-cloud-connector-e9f41d6.md "If you want to use Cloud Connector to establish the connection between your source system and SAP Data Intelligence Cloud, there are the
		following additional aspects to be kept in mind:")**  
If you want to use Cloud Connector to establish the connection between your source system and SAP Data Intelligence Cloud, there are the following additional aspects to be kept in mind:

