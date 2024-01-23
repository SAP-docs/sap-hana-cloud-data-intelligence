<!-- loiode1481f9a63c42989c36522aa981177b -->

# Availability of the Node.js Subengine SDK

The Node.js SDK is included into the Node.js subengine, but you can also download and install it.

Configure any Node.js operator to require the Node.js SDK at runtime. The Node.js operator uses the Node.js subengine SDK module named `'@sap/vflow-sub-node-sdk'` as follows:

```
const { operator } = require("@sap/vflow-sub-node-sdk");
const operator = Operator.getInstance();
```

However, if you use a dedicated local Node.js development project, download and install the Node.js subengine SDK so that you can program against its API.

