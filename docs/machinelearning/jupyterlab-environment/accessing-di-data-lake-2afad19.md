<!-- loio2afad19a621342508b0c95da4576df11 -->

# Accessing DI\_DATA\_LAKE

Learn how to access data sets stored in the DI\_DATA\_LAKE connection directly from your Jupyter notebook.

> ### Recommendation:  
> Use the DI\_DATA\_LAKE connection to store all large files and artifacts. Creating large files inside the Jupyter file system can cause issues with version creation and is best avoided.

You can access data sets that are stored in the DI\_DATA\_LAKE connection directly from your Jupyter notebook. To do so, start by installing HDFS. Then submit an HTTP request to the end point `http://datalake:50070`. You can base your request on the following code:

```py
!pip install hdfs

from hdfs import InsecureClient

client = InsecureClient('http://datalake:50070')
client.status("/")
```

For an external connection, refer to the following example:

```py
!pip install hdfs

from hdfs import InsecureClient

client = InsecureClient('http://datalake:50070')
client.status("/external/<connection_id>/")
```

The *<connection\_id\>* is the value of the connection you created in the Connection Management interface \(also displayed in the *Connection ID* column\). Calls to this endpoint are secure.

**Related Information**  


[SDL (Semantic Data Lake)](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/a6b555f56d8c4641bd1a248231202050.html "The SDL connection type connects to and accesses information from remote object stores.") :arrow_upper_right:

[Storage Gateway API](https://api.sap.com/api/storagegateway/resource)

[HdfsCLI](https://hdfscli.readthedocs.io/en/latest/)

