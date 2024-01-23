<!-- loioc4363909f000491b9fe191c68b86dd46 -->

# OpenAPI PlainClient Demo

The openapi.client operator can call arbitrary REST services from a graph.



<a name="loioc4363909f000491b9fe191c68b86dd46__section_w4x_mhb_v2b"/>

## Configure and Run the Graph

Follow the steps below to run the example from the SAP Data Intelligence Modeler UI:

1.  Start the openapi.server plain\_greeter demo graph \(com.sap.demo.openapi.server.plain\_greeter\), which exposes its service at path /openapi/service/samples/plain\_greeter relative to the Modeler instance URL.
2.  Verify the host and port configured for this demo graph matches the actual Modeler instance.
3.  Start this demo graph, which will automatically start invoking a series of operations.
4.  Open the UI from the wiretap operator so that the response messages from the invoked operations are displayed on the browser.

