<!-- loiof4310e526be14965a4e099f00bd993e0 -->

# OpenAPI Greeter Demo

The openapi.server operator allows REST services to be exposed from a graph. It can expose the endpoint as a Swagger-driven service endpoint or a plain REST service endpoint. This example demonstrates its Swagger-driven mode. The exposed service is described by a Swagger document and the request messages are handled based on this document.



<a name="loiof4310e526be14965a4e099f00bd993e0__section_w4x_mhb_v2b"/>

## Configure and Run the Graph

Follow the steps below to run the example from the SAP Data Intelligence Modeler UI:

1.  Start the graph. This demo service will be started at path /openapi/service/samples/greeter relative to the Modeler instance URL.
2.  Open the UI from the wiretap operator so that the request messages are displayed on the browser.
3.  Open the URL /openapi/service/samples/greeter/swagger.json to retrieve its Swagger document. \(If you are using Chrome Swagger-plugin, you can directly view this document and invoke the operations. Otherwise, use another tool to invoke these REST operations described in the document.\)

For example, when using curl, these correspond to:

```
curl http://{host}:{port}/{path}/openapi/service/samples/greeter/v1/ping

curl -X -d 'some text' http://{host}:{port}/{path}/openapi/service/samples/greeter/v1/echo
```

The implementation of the operations can be found in the script operator.

