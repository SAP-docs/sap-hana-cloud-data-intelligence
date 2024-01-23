<!-- loioe9f41d6e7ffb4fcab0715db424ff47c7 -->

# Establishing a Connection Using Cloud Connector

If you want to use Cloud Connector to establish the connection between your source system and SAP Data Intelligence Cloud, there are the following additional aspects to be kept in mind:

-   Consider the general information provided under [SAP BTP Connectivity](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e54cc8fbbb571014beb5caaf6aa31280.html?q=sap%20btp%20connectivity) in the SAP Help Portal as well as the additional information about [Using SAP Cloud Connector Gateway](https://help.sap.com/viewer/ca509b7635484070a655738be408da63/Cloud/en-US/261f792192a949e0b0f18c5ab5a48cff.html) in the context of SAP Data Intelligence Cloud.

-   It is important that the SSC gateway is registered with SAP Data Intelligence Cloud. \(This should happen automatically when you run SAP Data Intelligence Cloud.\)

-   To be able to use an ABAP connection with Secure Network Communication \(SNC\) with Cloud Connector, you need to configure SNC in Cloud Connector \(not in the connection management for SAP Data Intelligence Cloud\).


To be able to work with Cloud Connector \(SCC\), you need to do the following:

-   Install and configure SCC using SAP Cloud Connectivity Platform \(as described under [SAP BTP Connectivity → Integration](https://help.sap.com/viewer/product/CP_CONNECTIVITY/Cloud/en-US)\). When doing so, consider the information provided in the installation guide and the configuration for Cloud Connector.

-   Add the SCC connection parameter `Gateway` in the connection management for SAP Data Intelligence Cloud.

-   In SCC, grant the functional access to the SAP NetWeaver ABAP function modules: Select the virtual host you want to use. A new pane called Resources of \[your host\] opens. On the new pane, choose the + symbol to add the required resources:

    -   For extracting data using CDS view extraction, add DHAMB\_/Prefix, DHAPE\_/Prefix, and RFC\_FUNCTION\_SEARCH.

    -   For extracting data based on tables with SAP LT Replication Server, add LTAMB\_/Prefix, LTAPE\_/Prefix, and RFC\_FUNCTION\_SEARCH.



