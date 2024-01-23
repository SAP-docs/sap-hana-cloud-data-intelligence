<!-- loio54d279dbd83640bcab2a2a077c103d67 -->

# OpenAPI Plain Greeter

The openapi.server operator allows REST services to be exposed from a graph. It can expose the endpoint as a Swagger-driven service endpoint or a plain REST service endpoint. This example demonstrates its plain service mode. There is no Swagger document associated with this service.



<a name="loio54d279dbd83640bcab2a2a077c103d67__section_w4x_mhb_v2b"/>

## Configure and Run the Graph

Follow the steps below to run the example from the SAP Data Intelligence Modeler UI:

1.  Start the graph. This demo service will be started at path /openapi/service/samples/plain\_greeter relative to the Modeler instance URL.
2.  Open the UI from the wiretap operator so that the request messages are displayed on the browser.
3.  From some REST client, send a GET request to /openapi/service/samples/plain\_greeter/v1/ping or a POST request to /openapi/service/samples/plain\_greeter/v1/echo with some text content, as in the greeter sample. In addition, there is another operation hosted at /openapi/service/samples/plain/\_greeter/v1/happy, which returns an HTTP response with either status 200 or 400 randomly. When using curl, these correspond to:

```
curl http://{host}:{port}{mountpath}/openapi/service/samples/plain_greeter/v1/ping

curl -X POST -d 'some text' http://{host}:{port}{mountpath}/openapi/service/samples/plain_greeter/v1/echo

curl -i http://{host}:{port}{mountpath}/openapi/service/samples/plain_greeter/v1/happy
```

For example, for a local Modeler instance:

```
$ curl http://localhost:8090/openapi/service/samples/plain_greeter/v1/ping
{"pong":5}

$ curl http://localhost:8090/openapi/service/samples/plain_greeter/v1/ping
{"pong":6}

$ curl -X POST -d 'Buenos dias' http://localhost:8090/openapi/service/samples/plain_greeter/v1/echo
{"echo":"Buenos dias"}

$ curl -i http://localhost:8090/openapi/service/samples/plain_greeter/v1/happy
HTTP/1.1 200 OK
...

{"status":"happy"}

$ curl -i http://localhost:8090/openapi/service/samples/plain_greeter/v1/happy
HTTP/1.1 400 Bad Request
...

{"status":"unhappy"}
```

The implementation of the operations can be found in the script operator.

