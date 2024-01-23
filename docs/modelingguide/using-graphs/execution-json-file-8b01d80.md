<!-- loio8b01d80adef14b67ab1dbc8a677232b1 -->

# execution.json File

The `execution.json` file contains information about the execution for a graph, such as groups, pods, processes \(operator instances in a graph\), and so on.

You can use the `execution.json` file to identify which pod or pods failed.

```
{
    "src": "com.sap.demo.datagenerator",
    "name": "com.sap.demo.datagenerator",
    "executionType": "stream",
    "handle": "9a6eeb59abb242baabb110dba50ae178",
    "status": "running",
    "terminationRequested": false,
    "message": "Graph is currently running",
    "remoteExecution": {
        "parent": ""
    },
    "started": 1535538401,
    "updated": 1535538405,
    "stopped": 0,
    "submitted": 1535538400,
    "allocations": [
        {
            "groupName": "default",
            "groupDescription": "",
            "subgraph": "default",
            "container": "vflow-graph-9a6eeb59abb242baabb110dba50ae178-com-sap-demo-ngq4m",
            "containerIp": "172.17.0.8",
            "host": "minikube",
            "status": "running",
            "message": "Container is currently running",
            "restartCount": 0,
            "image": "a-docker-registry:5000/vora/vflow-node:2.3.30-dev-0829-com.sap.debian",
            "destination": "",
            "updated": "2018-08-29T10:26:40Z",
            "processes": [
                {
                    "id": "16d1",
                    "componentId": "com.sap.system.jsengine",
                    "status": "running",
                    "processName": "datagenerator (16d1)",
                    "engine": "main",
                    "timestampPublished": "2018-08-29T10:26:41Z",
                    "timestampReceived": "2018-08-29T10:26:41.031657526Z",
                    "published": 1535538401,
                    "received": 1535538401,
                    "message": "Process is running",
                    "metrics": null
                },
                {
                    "id": "1mnu",
                    "componentId": "com.sap.system.terminal",
                    "status": "running",
                    "processName": "terminal (1mnu)",
                    "engine": "main",
                    "timestampPublished": "2018-08-29T10:26:41Z",
                    "timestampReceived": "2018-08-29T10:26:41.033268298Z",
                    "published": 1535538401,
                    "received": 1535538401,
                    "message": "Process is running",
                    "metrics": null
                }
            ]
        }
    ]
}
```

