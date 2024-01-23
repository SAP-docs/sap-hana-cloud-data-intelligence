<!-- loio5335ef13d9864c5c8c5b7e0ad47a5221 -->

# DQMm Reverse Geo

Start this demo graph, which will automatically start invoking a series of operations.



<a name="loio5335ef13d9864c5c8c5b7e0ad47a5221__section_ynb_kpf_dfb"/>

## Prerequisites

-   Subscription to the Data Quality Management, microservices for location data service.



<a name="loio5335ef13d9864c5c8c5b7e0ad47a5221__section_lmw_t4f_dfb"/>

## Configure and Run the Graph

Perform the following steps to run the example from the SAP Data Intelligence Modeler user interface:

1.  Start the DQMm Reverse Geo demo graph \(com.sap.demo.dqmm.reverseGeo\).
2.  Set the host of the DQMm application URL in the DQMm Client operator.
3.  Choose either to authenticate using basic or oauth. You can use basic if you are accessing your subscription from your account on Trial. Use oauth if you are accessing your subscription from your account on a Factory landscape.
4.  If you are using ouath, log into your SAP BTP account and create an OAuth client for your subscription.
5.  In the DQMm Client operator, set the OAuth Token URL, Client ID, and the Client Secret.
6.  By default, the graph writes the output to the `/tmp` folder. Change this if you want the result written to another folder.
7.  Start the demo graph, which automatically starts invoking a series of operations.

