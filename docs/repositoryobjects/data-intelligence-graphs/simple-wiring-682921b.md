<!-- loio682921be45cc42f9aa665979569e7d0d -->

# Simple Wiring

Some operators are capable of connecting multiple connections from and to a single port as well as connecting between different port types that are supported by the automatic conversion of the pipeline engine. This graph directly connects three data generating operators of different output port types to a wiretap that is directly connected to a terminal and another wiretap.



## Prerequisites

Optional: basic understanding of REST services and OpenAPI 2.0



<a name="loio682921be45cc42f9aa665979569e7d0d__section_apn_csx_xkb"/>

## Configure and Run the Graph

Follow the steps below to run the example from the Data Pipeline UI:

1.  Start the graph. This demo service will be started at path /openapi/service/test/smart-wiring relative to the pipeline instance URL.

2.  Open the UI from Wiretap 1 and Terminal to see data from Data Generator and Message Generator are shown.

3.  Optional: open the UI from OpenAPI Message to see its Swagger Specification and invoke the service.


