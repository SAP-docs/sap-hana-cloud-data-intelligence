<!-- loio575cd079a1654a129b8989f4e36574f6 -->

# OpenAPI Middleware Demo

The openapi.server and openapi.client operators can be used to create a pipeline that can receive REST requests, filter, modify, and route the requests to external REST services and, finally, return the responses to the client. In particular, this demo graph receives REST requests at its own service path and forwards the requests to the greeter demo graph’s service path to invoke the corresponding greeter service operations.



<a name="loio575cd079a1654a129b8989f4e36574f6__section_fg3_t52_svb"/>

## Prerequisites

-   Basic understanding of REST servics and [OpenAPI 2.0](https://swagger.io/specification/v2/).



-   Familiarity with available REST clients to invoke the service.
-   Familiarity with [OpenAPI Greeter Demo](openapi-greeter-demo-f4310e5.md), which is used in this demo.



<a name="loio575cd079a1654a129b8989f4e36574f6__section_pv4_ks2_svb"/>

## Configure and Run the Graph

Follow the steps below to run the example from the Data Pipeline UI:

1.  Start the [OpenAPI Greeter Demo](openapi-greeter-demo-f4310e5.md) graph \(com.sap.demo.openapi.server.greeter\), which exposes its service at path `/openapi/service/samples/greeter` relative to the pipeline instance URL. This is the backend REST service.

2.  Verify if this service is working. \(Refer to the documenation for the [OpenAPI Greeter Demo](openapi-greeter-demo-f4310e5.md)\).

3.  Verify if the host and port configured for this demo graph’s openapi.client matches the actual instance. For example, if the greeter demo graph is running on localhost:8090 without any authentication, no adjustment is required. However, if the greeter demo graph is running in a cluster, these properties need to be adjusted accordingly along with its authentication scheme to be able to access the service.

4.  Start this openapi.middleware greeter demo graph, which exposes its service `/openapi/service/samples/middleware_greeter` relative to the pipeline instance URL.

5.  Invoke some REST operations. \(Refer to the available operations of the greeter demo graph, for example, from the browser or using curl.\)


For example, when using curl, you can call the greeter’s operations with

```
curl http[s]://{host}:{port}{mountpath}/openapi/service/samples/middleware_greeter/v1/ping

curl -X POST -d 'some text' http[s]://{host}:{port}{mountpath}/openapi/service/samples/middleware_greeter/v1/echo
```

For example, for a local instance \(host=localhost;port=8090;mountpath=;\)

```
$ curl http://localhost:8090/openapi/service/samples/middleware_greeter/v1/ping
{"pong":0}

$ curl http://localhost:8090/openapi/service/samples/middleware_greeter/v1/ping
{"pong":1}

$ curl -X POST -d 'Buenos dias' http://localhost:8090/openapi/service/samples/middleware_greeter/v1/echo
{"echo":"Buenos dias"}
```

