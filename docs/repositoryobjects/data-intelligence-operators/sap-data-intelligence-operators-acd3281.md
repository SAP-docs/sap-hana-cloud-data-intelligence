<!-- loioacd32810819a4b2893c9f8698e2ec55c -->

# SAP Data Intelligence Operators

SAP Data Intelligence provides built-in operators, that you can use directly in a graph or as the basis for creating a custom operator.

An event from the environment comes to a graph as a message that is delivered to an operator through its input ports. The operator interacts with the environment through its output ports. The operators are unaware of the graph in which they are defined and the source and target of their incoming and outgoing connections.

For information about using SAP Data Intelligence operators and creating your own custom operators, see [Using Operators](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/84e1df1ac115413da64b622ca779a424.html "Operators represent vertexes in a graph (pipeline) and are components that react to events configured in the graph environment.") :arrow_upper_right: in the *Modeling Guide*.

> ### Note:  
> -   Some of the SAP Data Intelligence operators have configuration type properties. SAP recommends that you choose *Configuration Manager* and select an existing connection ID.
> -   The following Gen1 and Gen2 operators work with the connections that you configure with the SAP Cloud Connector gateway:
> 
> 
>     <table>
>     <tr>
>     <th valign="top">
> 
>     Generation 1
>     
>     </th>
>     <th valign="top">
> 
>     Generation 2
>     
>     </th>
>     </tr>
>     <tr>
>     <td valign="top">
>     
>     -   ABAP operators
>     -   SAP HANA Client
>     -   SAP HANA Monitor
>     -   OpenAPI Client
>     -   HTTP Client
>     -   Kafka operators
> 
> 
>     
>     </td>
>     <td valign="top">
>     
>     -   ABAP operators
>     -   HANA operators
>     -   Kafka operators
> 
> 
>     
>     </td>
>     </tr>
>     </table>

The following table lists all operators and their primary use case. For more information about the operator, use the links in the table.

****


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Operator

</th>
<th valign="top">

ID

</th>
<th valign="top">

Primary Use Case

</th>
<th valign="top">

Status

</th>
<th valign="top">

Replaced By

</th>
</tr>
<tr>
<td valign="top">

[ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md)

</td>
<td valign="top">

[ABAP Converter](abap-converter-d58c19e.md)

</td>
<td valign="top">

com.sap.abap.toStringConverter

</td>
<td valign="top">

Convert a generic ABAP data type to string using the CSV, JSON, or XML format.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ABAP](abap-0f55b37.md)

</td>
<td valign="top">

[Read Data From SAP System](read-data-from-sap-system-d7dfd72.md)

</td>
<td valign="top">

com.sap.abap.reader

</td>
<td valign="top">

Read data from an ABAP system.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md)

</td>
<td valign="top">

[ABAP CDS Reader](abap-cds-reader-df331fc.md)

</td>
<td valign="top">

com.sap.abap.cds\_reader

</td>
<td valign="top">

Read data from a Core Data Services \(CDS\) view.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md)

</td>
<td valign="top">

[SLT Connector](slt-connector-ac5b713.md)

</td>
<td valign="top">

com.sap.abap.slt\_reader

</td>
<td valign="top">

Establish connections between SAP Landscape Transformation Replication Server \(SLT\) and SAP Data Intelligence.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md)

</td>
<td valign="top">

[Cluster Table Splitter](cluster-table-splitter-aefc6b9.md)

</td>
<td valign="top">

com.sap.abap.cluster\_splitter

</td>
<td valign="top">

Use SLT Connector to replicate one or more \(but not all\) logical tables for a cluster table.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md)

</td>
<td valign="top">

[Custom ABAP Operator](custom-abap-operator-bd79a31.md)

</td>
<td valign="top">

com.sap.abap.custom

</td>
<td valign="top">

Adapt to the selected custom operator implementation in the remote ABAP system.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md)

</td>
<td valign="top">

[ABAP ODP Reader](abap-odp-reader-d4c18f8.md)

</td>
<td valign="top">

com.sap.abap.odp.read

</td>
<td valign="top">

Read data from an object for operational data processing \(ODP\).

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md)

</td>
<td valign="top">

[SAP ABAP Operator](sap-abap-operator-8895172.md)

</td>
<td valign="top">

com.sap.abap.sap

</td>
<td valign="top">

Adapt to the selected standard operator implementation in the remote ABAP system.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Copy File \(Deprecated\)](copy-file-deprecated-9a9319a.md)

</td>
<td valign="top">

com.sap.storage.copy2

</td>
<td valign="top">

Copy files in a storage service.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[AWS SNS Consumer](aws-sns-consumer-b5f5445.md)

</td>
<td valign="top">

com.sap.cloud.aws.sns.consumer

</td>
<td valign="top">

Consume publications from an Amazon Web Services Simple Notification Service \(AWS SNS\) topic and output them as a stream of messages.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[AWS SNS Producer](aws-sns-producer-2d49ace.md)

</td>
<td valign="top">

com.sap.cloud.aws.sns.producer

</td>
<td valign="top">

Receive a message from the input port and publish it to an AWS SNS topic.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[Google Pub/Sub Consumer](google-pub-sub-consumer-68835e2.md)

</td>
<td valign="top">

com.sap.cloud.gcp.pubsub.consumer

</td>
<td valign="top">

Consume publications from a Google Pub/Sub topic and output them as a stream of messages.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[Google Pub/Sub Producer](google-pub-sub-producer-4da5bb4.md)

</td>
<td valign="top">

com.sap.cloud.gcp.pubsub.producer

</td>
<td valign="top">

Receive a message from the input port and publish it to a Google Pub/Sub topic.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[SAP HANA Client](sap-hana-client-c25dff3.md)

</td>
<td valign="top">

com.sap.hana.client2

</td>
<td valign="top">

Execute SQL statements and inserts CSV or JSON data into an SAP HANA instance.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[SAP HANA Monitor](sap-hana-monitor-9de323a.md)

</td>
<td valign="top">

com.sap.hana.monitor2

</td>
<td valign="top">

 

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[HTTP Client](http-client-f6619b1.md)

</td>
<td valign="top">

com.sap.http.client2

</td>
<td valign="top">

Send arbitrary HTTP requests, polling a URL, and posting JSON data.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[HTTP Server](http-server-8677737.md)

</td>
<td valign="top">

com.sap.http.server2

</td>
<td valign="top">

Start an HTTP server on a configurable port. It handles GET and POST requests received from a configurable handler path.Create a trigger on a given table. For each row inserted, save a copy in a temporary table and poll it for those new rows.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

-   [Kafka Consumer V1](kafka-consumer-v1-582b188.md)
-   [Kafka Consumer V2](kafka-consumer-v2-6d4be10.md)



</td>
<td valign="top">

-   com.sap.kafka.consumer2
-   com.sap.kafka.consumer2.v2



</td>
<td valign="top">

Consume records and messages from a Kafka cluster.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

-   [Kafka Producer V1](kafka-producer-v1-aecfaf2.md)
-   [Kafka Producer V2](kafka-producer-v2-e22d0e5.md)



</td>
<td valign="top">

-   com.sap.kafka.producer

-   com.sap.kafka.producer.v2



</td>
<td valign="top">

Send records and messages to topics on a Kafka cluster.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[MQTT Consumer](mqtt-consumer-709a1b6.md)

</td>
<td valign="top">

com.sap.mqtt.consumer

</td>
<td valign="top">

Subscribe to MQTT topics, consume its messages, and output them.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[MQTT Producer](mqtt-producer-c0ca754.md)

</td>
<td valign="top">

com.sap.mqtt.producer

</td>
<td valign="top">

Receive MQTT messages from a port and publish them in a topic.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[NATS Consumer](nats-consumer-d2a345d.md)

</td>
<td valign="top">

com.sap.nats.consumer

</td>
<td valign="top">

Consume messages from NATS and forward them to the output port.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[NATS Producer](nats-producer-e7fd7de.md)

</td>
<td valign="top">

com.sap.nats.producer

</td>
<td valign="top">

Receive a message from the input port and publish it into NATS.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[OpenAPI Client](openapi-client-8a70738.md)

</td>
<td valign="top">

com.sap.openapi.client

</td>
<td valign="top">

Invoke services described in a swagger/openAPI document.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[OpenAPI Server](openapi-server-1e23998.md)

</td>
<td valign="top">

com.sap.openapi.server

</td>
<td valign="top">

Provide services described in swagger/openAPI or unspecified HTTP services in Modeler.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[Receive Email](receive-email-f065059.md)

</td>
<td valign="top">

com.sap.email.receive

</td>
<td valign="top">

Receive emails.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[Send Email](send-email-8da19b1.md)

</td>
<td valign="top">

com.sap.email.send

</td>
<td valign="top">

Send emails.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="4775c2eba1d1460b8be6c7933d6c24e6.xml" text="" desc="" xtrc="xref:60" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

com.sap.social.tweetStream2

</td>
<td valign="top">

Create a trigger on a given table. For each row inserted, save a copy in a temporary table and poll it for thoseReceive a stream of tweets filtered by some keywords specified in the configuration using the Twitter Streaming API.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[WAMP Consumer](wamp-consumer-de1740e.md)

</td>
<td valign="top">

com.sap.wamp.consumer

</td>
<td valign="top">

Access records from Web Application Messaging Protocol \(WAMP\).

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-b12fb5d.md)

</td>
<td valign="top">

[WAMP Producer](wamp-producer-f6479fe.md)

</td>
<td valign="top">

com.sap.wamp.producer

</td>
<td valign="top">

Write files to Web Application Messaging Protocol \(WAMP\).

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Move File \(Deprecated\)](move-file-deprecated-205802e.md)

</td>
<td valign="top">

com.sap.storage.move2

</td>
<td valign="top">

Move \(rename\) files in a file service.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Read File \(Deprecated\)](read-file-deprecated-df00daf.md)

</td>
<td valign="top">

com.sap.storage.read

</td>
<td valign="top">

Read a file or periodically polls a directory for its contents in a storage service.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Remove File \(Deprecated\)](remove-file-deprecated-6f7c02d.md)

</td>
<td valign="top">

com.sap.storage.remove2

</td>
<td valign="top">

Remove files in a storage service.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Write File \(Deprecated\)](write-file-deprecated-43e1cc8.md)

</td>
<td valign="top">

com.sap.storage.write

</td>
<td valign="top">

Write files to a storage service.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

[Write File](write-file-7c3672c.md)

com.sap.file.write

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Azure SQL DB SQL Consumer \(Deprecated\)](azure-sql-db-sql-consumer-deprecated-ee69a3f.md)

</td>
<td valign="top">

com.sap.dh.ds.azuresqldb.sql.consumer

</td>
<td valign="top">

Perform a SQL query in an Azure SQL Database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Azure SQL DB Table Consumer \(Deprecated\)](azure-sql-db-table-consumer-deprecated-e9b708d.md)

</td>
<td valign="top">

com.sap.dh.ds.azuresqldb.table.consumer

</td>
<td valign="top">

Read from an Azure SQL Database table or view.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[DB2 SQL Consumer \(Deprecated\)](db2-sql-consumer-deprecated-4bbba4b.md)

</td>
<td valign="top">

com.sap.dh.ds.db2.sql.consumer

</td>
<td valign="top">

Perform a SQL query in a DB2 database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[DB2 Table Consumer \(Deprecated\)](db2-table-consumer-deprecated-42e6f7a.md)

</td>
<td valign="top">

com.sap.dh.ds.db2.table.consumer

</td>
<td valign="top">

Read from a DB2 table or view.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Flowagent CSV Producer](flowagent-csv-producer-eb59df8.md)

</td>
<td valign="top">

com.sap.dh.ds.csv.producer

</td>
<td valign="top">

Read any Flowagent-based consumer operator and output in a CSV format conforming to the RFC-4180 specification.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Flowagent File Producer \(Deprecated\)](flowagent-file-producer-deprecated-76e9d5c.md)

</td>
<td valign="top">

com.sap.dh.ds.storage.producer

</td>
<td valign="top">

Consume Flowagent-based consumer operators

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

-   [Flowagent SQL Executor V1 \(Deprecated\)](flowagent-sql-executor-v1-deprecated-d614ce5.md)
-   [Flowagent SQL Executor V2](flowagent-sql-executor-v2-9958a65.md)



</td>
<td valign="top">

-   com.sap.dh.ds.sql.executor
-   com.sap.dh.ds.sql.executor.v2



</td>
<td valign="top">

Perform an SQL Statement to any supported database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Flowagent Table Producer \(Deprecated\)](flowagent-table-producer-deprecated-fda7323.md)

</td>
<td valign="top">

com.sap.dh.ds.table.producer

</td>
<td valign="top">

Read from any Flowagent-based consumer operator and write in a table of any supported database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Google BigQuery SQL Consumer \(Deprecated\)](google-bigquery-sql-consumer-deprecated-67d243f.md)

</td>
<td valign="top">

com.sap.dh.ds.gbq.sql.consumer

</td>
<td valign="top">

Perform a SQL query to a Google BigQuery table.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Google BigQuery Table Loader](google-bigquery-table-loader-b8b1e5e.md)

</td>
<td valign="top">

com.sap.dh.ds.gbq.producer

</td>
<td valign="top">

Write to a Google BigQuery table.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[HANA Table Consumer \(Deprecated\)](hana-table-consumer-deprecated-e253728.md)

</td>
<td valign="top">

com.sap.dh.ds.hanaodbc.table.consumer

</td>
<td valign="top">

Read from a HANA table or view using a Flowagent subengine.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[MySQL SQL Consumer \(Deprecated\)](mysql-sql-consumer-deprecated-7ffaaee.md)

</td>
<td valign="top">

com.sap.dh.ds.mysql.sql.consumer

</td>
<td valign="top">

Perform a SQL query in a MySQL database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[MySQL Table Consumer \(Deprecated\)](mysql-table-consumer-deprecated-973e643.md)

</td>
<td valign="top">

com.sap.dh.ds.mysql.table.consumer

</td>
<td valign="top">

Read from a MySQL table or view.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[OData Query Consumer](odata-query-consumer-7da3182.md)

</td>
<td valign="top">

com.sap.dh.sdi.odata.table.consumer

</td>
<td valign="top">

Read from an OData RESTful API.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[ODBC SQL Consumer \(Deprecated\)](odbc-sql-consumer-deprecated-249c098.md)

</td>
<td valign="top">

com.sap.dh.ds.odbc.sql.consumer

</td>
<td valign="top">

Perform a SQL query to any database that provides an Open Database Connectivity \(ODBC\) connector.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[ODBC Table Consumer \(Deprecated\)](odbc-table-consumer-deprecated-231a007.md)

</td>
<td valign="top">

com.sap.dh.ds.odbc.table.consumer

</td>
<td valign="top">

Read a table from any database that provides an Open Database Connectivity \(ODBC\) connector.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Open Connectors SQL Consumer](open-connectors-sql-consumer-966c4d1.md)

</td>
<td valign="top">

com.sap.dh.sdi.openconnectors.sql.consumer

</td>
<td valign="top">

Get and filter data by the given SQL statement from SAP BTP Open Connectors.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Open Connectors Table Consumer \(Deprecated\)](open-connectors-table-consumer-deprecated-3a8fd0e.md)

</td>
<td valign="top">

com.sap.dh.sdi.openconnectors.table.consumer

</td>
<td valign="top">

Get all data from the given table name from SAP BTP Open Connectors.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Oracle Table Consumer \(Deprecated\)](oracle-table-consumer-deprecated-42350ab.md)

</td>
<td valign="top">

com.sap.dh.ds.oracle.table.consumer

</td>
<td valign="top">

Read from an Oracle table or view.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Oracle SQL Consumer \(Deprecated\)](oracle-sql-consumer-deprecated-9ed0ea4.md)

</td>
<td valign="top">

com.sap.dh.ds.oracle.sql.consumer

</td>
<td valign="top">

Perform a SQL query in an Oracle database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[CDC Graph Generator \(Deprecated\)](cdc-graph-generator-deprecated-a69c62f.md)

</td>
<td valign="top">

com.sap.dh.cdc.graphGenerator

</td>
<td valign="top">

Generate three graphics by doing static analyses of the metadata of the source table.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

[Table Replicator V3 \(Deprecated\)](table-replicator-v3-deprecated-79fcadb.md)

com.sap.database.table.replicator

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[SAP IQ SQL Consumer \(Deprecated\)](sap-iq-sql-consumer-deprecated-38e8752.md)

</td>
<td valign="top">

com.sap.dh.ds.sapiq.sql.consumer

</td>
<td valign="top">

Perform an SQL query to an SAP IQ database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[SAP IQ Table Consumer \(Deprecated\)](sap-iq-table-consumer-deprecated-3588a95.md)

</td>
<td valign="top">

com.sap.dh.ds.sapiq.table.consumer

</td>
<td valign="top">

Read from an SAP IQ table or view.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[SQL Server SQL Consumer \(Deprecated\)](sql-server-sql-consumer-deprecated-4b570d4.md)

</td>
<td valign="top">

com.sap.dh.ds.microsoftsqlserver.sql.consumer

</td>
<td valign="top">

Perform an SQL query to an SQL Server database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[SQL Server Table Consumer \(Deprecated\)](sql-server-table-consumer-deprecated-53bd4da.md)

</td>
<td valign="top">

com.sap.dh.ds.microsoftsqlserver.table.consumer

</td>
<td valign="top">

Read from an SQL Server table or view.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity \(via Flowagent\)](connectivity-via-flowagent-4055624.md)

</td>
<td valign="top">

[Table Replicator V3 \(Deprecated\)](table-replicator-v3-deprecated-79fcadb.md)

</td>
<td valign="top">

com.sap.database.table.replicator

</td>
<td valign="top">

Capture the delta and handle applying the changes to a target table, allowing replication of tables in an efficient and secure way, through an in-built recovery mechanism.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Converter](converter-8f8ede5.md)

</td>
<td valign="top">

[StreamToString Converter](streamtostring-converter-e00cbeb.md)

</td>
<td valign="top">

com.sap.util.streamToStringConverter

</td>
<td valign="top">

Parse a contiguous stream and output strings that are separated by platform-dependent line delimiters.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Converter](converter-8f8ede5.md)

</td>
<td valign="top">

[StringToStream Converter](stringtostream-converter-a59d48f.md)

</td>
<td valign="top">

com.sap.util.stringToStreamConverter

</td>
<td valign="top">

Convert incoming messages of type 'string' to a contiguous stream.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Converter](converter-8f8ede5.md)

</td>
<td valign="top">

[ToBlob Converter](toblob-converter-6dd943c.md)

</td>
<td valign="top">

com.sap.util.toBlobConverter

</td>
<td valign="top">

Convert the input into a byte array.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Converter](converter-8f8ede5.md)

</td>
<td valign="top">

[ToMessage Converter](tomessage-converter-eee668e.md)

</td>
<td valign="top">

com.sap.util.toMessageConverter

</td>
<td valign="top">

Convert the input to a Modeler message.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Converter](converter-8f8ede5.md)

</td>
<td valign="top">

[ToNumber Converter](tonumber-converter-1508faf.md)

</td>
<td valign="top">

com.sap.util.toNumberConverter

</td>
<td valign="top">

Convert types int64, uint64, float64, and string into other numeric types.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Converter](converter-8f8ede5.md)

</td>
<td valign="top">

[ToString Converter](tostring-converter-fdd883c.md)

</td>
<td valign="top">

com.sap.util.toStringConverter

</td>
<td valign="top">

Convert the input to a string.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Converter](converter-8f8ede5.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="0c99a8b7ee9349a4839b47c81ca74c0a.xml" text="" desc="" xtrc="xref:141" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

com.sap.vgui.conversion.toStringType

</td>
<td valign="top">

Convert regular types to the specialized string types used for Scenes.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Quality](data-quality-7cd1631.md)

</td>
<td valign="top">

[Anonymization](anonymization-db0245a.md)

</td>
<td valign="top">

com.sap.demo.anonymization

</td>
<td valign="top">

Protect the privacy of individuals by creating groups of similar records.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Quality](data-quality-7cd1631.md)

</td>
<td valign="top">

[Data Mask](data-mask-6c73a5f.md)

</td>
<td valign="top">

com.sap.dh.dq.dataMask

</td>
<td valign="top">

Protect the personally identifiable or sensitive information by covering all or a portion of the data.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Quality](data-quality-7cd1631.md)

</td>
<td valign="top">

[DQMm Address Cleanse](dqmm-address-cleanse-0e718a1.md)

</td>
<td valign="top">

com.sap.dh.dq.dqmmAddressCleanse

</td>
<td valign="top">

Prepare address cleanse requests to be sent to SAP Data Quality Management, microservices for location data.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Quality](data-quality-7cd1631.md)

</td>
<td valign="top">

[DQMm Client](dqmm-client-35e476a.md)

</td>
<td valign="top">

com.sap.dh.dq.dqmmClient

</td>
<td valign="top">

Send requests to Data Quality Management, microservices for location data.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Quality](data-quality-7cd1631.md)

</td>
<td valign="top">

[DQMm Reverse Geo](dqmm-reverse-geo-ceda9b9.md)

</td>
<td valign="top">

com.sap.dh.dq.dqmmReverseGeo

</td>
<td valign="top">

Prepare address cleanse requests to be sent to SAP Data Quality Management, microservices for location data.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Quality](data-quality-7cd1631.md)

</td>
<td valign="top">

[Person and Firm Cleanse](person-and-firm-cleanse-ab68be3.md)

</td>
<td valign="top">

com.sap.dh.dq.personAndFirmCleanse

</td>
<td valign="top">

Identify the names of people and firms even when both types of names are in the same column.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Quality](data-quality-7cd1631.md)

</td>
<td valign="top">

-   [Validation Rule](validation-rule-ef777b7.md)
-   [Validation Rule V2](validation-rule-v2-cec2a76.md)



</td>
<td valign="top">

-   com.sap.dh.dq.validationRule
-   com.sap.dh.dq.validationRule.v2



</td>
<td valign="top">

Create rules and routes records that pass through the Pass output port.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[Data Transfer](data-transfer-40c0ec9.md)

</td>
<td valign="top">

com.sap.dh.bwdatatransfer

</td>
<td valign="top">

Transfer data from an SAP BW system to major cloud storages

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[BW Process Chain](bw-process-chain-4dc570a.md)

</td>
<td valign="top">

com.sap.dh.bwprocesschain

</td>
<td valign="top">

Help execute an SAP BW process chain in an SAP BW system.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[HANA Flowgraph](hana-flowgraph-f9f9908.md)

</td>
<td valign="top">

com.sap.dh.hanaflowgraph

</td>
<td valign="top">

Execute an SAP HANA flowgraph in an SAP HANA system.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="9048e6813b254be6b117658d676cc6cc.xml" text="" desc="" xtrc="xref:166" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

com.sap.dh.datatransform

</td>
<td valign="top">

Provide capabilities to meet your data transformation requirement.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

[Data Transform V2](data-transform-v2-a415f61.md)

com.sap.datatransform

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[Notification](notification-6a7d923.md)

</td>
<td valign="top">

com.sap.dh.notification

</td>
<td valign="top">

Send email notifications at certain points in the data workflow execution.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[Pipeline](pipeline-4525f87.md)

</td>
<td valign="top">

com.sap.dh.vflowpipeline

</td>
<td valign="top">

Execute a Modeler flow in an SAP Data Intelligence system.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[SAP Data Services Job](sap-data-services-job-539680c.md)

</td>
<td valign="top">

com.sap.dh.dsjob

</td>
<td valign="top">

Execute an SAP Data Services job in a remote system.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[Workflow Merge \(and\)](workflow-merge-and-871a5ca.md)

</td>
<td valign="top">

com.sap.dh.logical.AND

</td>
<td valign="top">

Control the flow of execution in a data workflow.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[Workflow Merge \(or\)](workflow-merge-or-6be13b9.md)

</td>
<td valign="top">

com.sap.dh.logical.OR

</td>
<td valign="top">

Control the flow of execution in a data workflow.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[Workflow Split](workflow-split-5b35309.md)

</td>
<td valign="top">

com.sap.dh.split

</td>
<td valign="top">

Duplicate an input message into two output messages.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[Workflow Terminator](workflow-terminator-8952b8d.md)

</td>
<td valign="top">

com.sap.dh.terminator

</td>
<td valign="top">

Shut down the data workflow execution.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Data Workflows](data-workflows-0cb7140.md)

</td>
<td valign="top">

[Workflow Trigger](workflow-trigger-e12de65.md)

</td>
<td valign="top">

com.sap.dh.trigger

</td>
<td valign="top">

Send a start message, which you can use to start a data workflow.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Files](files-00ddc0a.md)

</td>
<td valign="top">

[From File](from-file-c33abdb.md)

</td>
<td valign="top">

com.sap.file.fromFile

</td>
<td valign="top">

Extract the path attribute from a file message.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Files](files-00ddc0a.md)

</td>
<td valign="top">

-   [List Files](list-files-7060368.md)
-   [List Files V2](list-files-v2-4d4da21.md)



</td>
<td valign="top">

-   com.sap.file.list
-   com.sap.file.list.v2



</td>
<td valign="top">

List files and directories from various storage services.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Files](files-00ddc0a.md)

</td>
<td valign="top">

[Monitor Files](monitor-files-e04a461.md)

</td>
<td valign="top">

com.sap.file.monitorFiles

</td>
<td valign="top">

Monitor file events in a directory from various storage services.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Files](files-00ddc0a.md)

</td>
<td valign="top">

[Read File](read-file-bf64491.md)

</td>
<td valign="top">

com.sap.file.read

</td>
<td valign="top">

Read the content of files from different storage services.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Files](files-00ddc0a.md)

</td>
<td valign="top">

[Remove File](remove-file-34ab7a6.md)

</td>
<td valign="top">

com.sap.file.removeFile

</td>
<td valign="top">

Remove files and directories from various storage services.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Files](files-00ddc0a.md)

</td>
<td valign="top">

[To File](to-file-20d5e26.md)

</td>
<td valign="top">

com.sap.file.toFile

</td>
<td valign="top">

Convert the input to a File type.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Files](files-00ddc0a.md)

</td>
<td valign="top">

-   [Write File](write-file-7c3672c.md)
-   [Binary File Producer](binary-file-producer-64d01ad.md)



</td>
<td valign="top">

-   com.sap.file.write
-   com.sap.file.write.v2



</td>
<td valign="top">

Write files to various services.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Files](files-00ddc0a.md)

</td>
<td valign="top">

-   [Binary File Consumer](binary-file-consumer-1faddfa.md)



</td>
<td valign="top">

com.sap.file.read.v2

</td>
<td valign="top">

Reads files from various services.

</td>
<td valign="top">

 

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Hadoop and Spark](hadoop-and-spark-cc1a434.md)

</td>
<td valign="top">

[Livy Spark Submit](livy-spark-submit-caf0066.md)

</td>
<td valign="top">

com.sap.livy.submit

</td>
<td valign="top">

Submit jobs to a cluster using the Livy REST API.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Hadoop and Spark](hadoop-and-spark-cc1a434.md)

</td>
<td valign="top">

[Submit Hadoop Job](submit-hadoop-job-f47eb92.md)

</td>
<td valign="top">

com.sap.hadoop.submitJob

</td>
<td valign="top">

Submit jobs to Hadoop clusters provided by different cloud providers.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Jupyter Operator](jupyter-operator-99f2fc3.md)

</td>
<td valign="top">

[Jupyter Operator](jupyter-operator-99f2fc3.md)

</td>
<td valign="top">

com.sap.jupyter

</td>
<td valign="top">

Launches a Jupyter notebook application where you can create notebooks to interact with the data flow using Python 3.9 code.

</td>
<td valign="top">

 

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[PA Automated \(Deprecated\)](pa-automated-deprecated-42452bd.md)

</td>
<td valign="top">

com.sap.ml.pa.automatedAnalytics

</td>
<td valign="top">

Apply the PA Automated Analytics product for prediction of values.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Model Consumer \(Deprecated\)](model-consumer-deprecated-281018c.md)

</td>
<td valign="top">

com.sap.ml.model.consumer

</td>
<td valign="top">

Consume a model in the model repository.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

[Artifact Consumer](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/18e47f9018904e1aae5107364884e24b.html "Receives the id of a registered artifact and outputs its metadata. It is intended to be followed by an operator to retrieve the artifact file(s) from the Semantic Data Lake (SDL). For an example of usage of this operator, refer to the Python Consumer template pipeline.") :arrow_upper_right:

com.sap.ml.artifact.consumer

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Model Producer \(Deprecated\)](model-producer-deprecated-98079cf.md)

</td>
<td valign="top">

com.sap.ml.model.producer

</td>
<td valign="top">

Push a model to the model repository.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

[Artifact Producer](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/9b8b01884a1e47c9a925e350fcc6b97f.html "The Artifact Producer operator registers the artifact (dataset, model or other) given as input and returns the artifact's generated ID.") :arrow_upper_right:

com.sap.ml.artifact.producer

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Command Executor](command-executor-50f0d5c.md)

</td>
<td valign="top">

com.sap.system.commandExecutor

</td>
<td valign="top">

Execute the given command for each arrival of a message on the stdin port.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Streaming Analytics Projects](streaming-analytics-projects-0b6100b.md)

</td>
<td valign="top">

com.sap.streamingproject

</td>
<td valign="top">

Represent a streaming analytics project.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Constant Generator](constant-generator-ec2bad5.md)

</td>
<td valign="top">

com.sap.util.constantGenerator

</td>
<td valign="top">

Represent a constant string that may be emitted into the graph.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Data Generator](data-generator-88a1dde.md)

</td>
<td valign="top">

com.sap.util.dataGenerator

</td>
<td valign="top">

Generate random sample data every 500 ms.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Go Message Operator](go-message-operator-aed6771.md)

</td>
<td valign="top">

com.sap.system.golangmengine2

</td>
<td valign="top">

Use the message type with a Go script.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Go Operator](go-operator-aabb1ca.md)

</td>
<td valign="top">

com.sap.system.golangExecutor2

</td>
<td valign="top">

Executes Go code within a graph.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Go String Operator](go-string-operator-fcc842c.md)

</td>
<td valign="top">

com.sap.system.golangengine2

</td>
<td valign="top">

Execute Go code within a graph.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[JavaScript Operator](javascript-operator-a591513.md)

</td>
<td valign="top">

com.sap.system.jsoperator

</td>
<td valign="top">

Execute JavaScript snippets within a graph.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[JavaScript \(v2\)](javascript-v2-ad5efc3.md)

</td>
<td valign="top">

com.sap.system.jsengine.v2

</td>
<td valign="top">

Execute JavaScript snippets within a graph and allow another part of the code to be executed until the blocking call returns.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[JS Message Operator](js-message-operator-05b590a.md)

</td>
<td valign="top">

com.sap.system.jsmengine

</td>
<td valign="top">

Use the message type with the JavaScript operator.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="83d3f1eb68944307bf424730b67220f0.xml" text="" desc="" xtrc="xref:237" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

com.sap.system.jsengine

</td>
<td valign="top">

Handle inputs and generate outputs.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Message Generator](message-generator-dada704.md)

</td>
<td valign="top">

com.sap.util.dataMessageGenerator

</td>
<td valign="top">

Generate a message with random sample data every 500 ms.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Node Base Operator](node-base-operator-36da115.md)

</td>
<td valign="top">

com.sap.node.operator

</td>
<td valign="top">

Support custom scripts in ECMAScript 2015 \(ES6\) based on Node.js.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Node Data Generator](node-data-generator-d2b7035.md)

</td>
<td valign="top">

com.sap.node.datagenerator

</td>
<td valign="top">

Mimic an IoT device and provides random data sets.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Node Message Counter](node-message-counter-9350899.md)

</td>
<td valign="top">

com.sap.node.counter

</td>
<td valign="top">

Implement a message counter using Node.js.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[Process Executor](process-executor-1283ae5.md)

</td>
<td valign="top">

com.sap.system.processExecutor

</td>
<td valign="top">

Start a process and provide given contiguous streams to it.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

-   [Python3 Operator](python3-operator-0211803.md)
-   [Python3 Operator V2](python3-operator-v2-1b5cca1.md)



</td>
<td valign="top">

-   com.sap.system.python3Operator
-   com.sap.system.python3Operator.v2



</td>
<td valign="top">

Define a script that offers some convenience functions provided by the API object.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

[R Client](r-client-0d9f275.md)

</td>
<td valign="top">

com.sap.system.rClient4

</td>
<td valign="top">

Run R code that you defined in the Rserve.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[R Client \(Deprecated\)](r-client-deprecated-30423dc.md)

</td>
<td valign="top">

com.sap.system.rClient3

</td>
<td valign="top">

Run R code defined by you in the Rserve.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="78779d33920d4226acb0bf0144bf9414.xml" text="" desc="" xtrc="xref:256" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

com.sap.system.process.stdmuxer

</td>
<td valign="top">

Map multiple input ports to stdin of a process and multiplex the output of stdout to multiple output ports.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Processing](processing-9aed46e.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="5b6c45202e0d4525b96df2f8532648f3.xml" text="" desc="" xtrc="xref:258" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

com.sap.streamingproject

</td>
<td valign="top">

Run a Streaming Analytics project.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Remote DataFlow](remote-dataflow-c575538.md)

</td>
<td valign="top">

-   [Data Services Transform](data-services-transform-4f7400e.md)
-   [Data Services Transform V2](data-services-transform-v2-7c92e98.md)



</td>
<td valign="top">

-   com.sap.dataservices.transform
-   com.sap.dataservices.transform.v2



</td>
<td valign="top">

Perform data transformations, such as projection, filter, and column operations and move data from on-premise source to SAP Data Intelligence.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP HANA](sap-hana-76ccc16.md)

</td>
<td valign="top">

-   [Initialize HANA Table](initialize-hana-table-200b932.md)

-   [Initialize HANA Table V2](initialize-hana-table-v2-5f52e92.md)




</td>
<td valign="top">

-   com.sap.hana.initTable

-   com.sap.hana.initTable.v2




</td>
<td valign="top">

Initialize one or more tables on an SAP HANA database

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP HANA](sap-hana-76ccc16.md)

</td>
<td valign="top">

-   [Read HANA Table](read-hana-table-19b8cde.md)

-   [Read HANA Table V2](read-hana-table-v2-b51aded.md)



</td>
<td valign="top">

-   com.sap.hana.readTable

-   com.sap.hana.readTable.v2



</td>
<td valign="top">

Read data from a table in SAP HANA.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP HANA](sap-hana-76ccc16.md)

</td>
<td valign="top">

-   [Run HANA SQL](run-hana-sql-cf17079.md)

-   [Run HANA SQL V2](run-hana-sql-v2-5796f97.md)



</td>
<td valign="top">

-   com.sap.hana.runSQL

-   com.sap.hana.runSQL.v2



</td>
<td valign="top">

Execute user-provided SQL statements on an SAP HANA database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP HANA](sap-hana-76ccc16.md)

</td>
<td valign="top">

-   [Write to HANA Table](write-to-hana-table-5c8d08d.md)

-   [Write HANA Table V2](write-hana-table-v2-b6a5c17.md)



</td>
<td valign="top">

-   com.sap.hana.writeTable

-   com.sap.hana.writeTable.v2



</td>
<td valign="top">

Ingest data into one or more tables on an SAP HANA database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Integration](sap-integration-12600c5.md)

</td>
<td valign="top">

[Cloud Data Integration Consumer](cloud-data-integration-consumer-f1f6af0.md)

</td>
<td valign="top">

com.sap.dh.cloud\_data\_integration

</td>
<td valign="top">

Use Flowagent for execution.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Integration](sap-integration-12600c5.md)

</td>
<td valign="top">

[SAP Analytics Cloud Formatter](sap-analytics-cloud-formatter-773374a.md)

</td>
<td valign="top">

com.sap.sac.formatter

</td>
<td valign="top">

Convert message.table input data to message format before sending to SAP Analytics Cloud.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Integration](sap-integration-12600c5.md)

</td>
<td valign="top">

[SAP Analytics Cloud Producer](sap-analytics-cloud-producer-e4d7cf6.md)

</td>
<td valign="top">

com.sap.sac.producer

</td>
<td valign="top">

Send data to the SAP Analytics Cloud application.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Integration](sap-integration-12600c5.md)

</td>
<td valign="top">

[SAP CP EM Consumer](sap-cp-em-consumer-a81089c.md)

</td>
<td valign="top">

com.sap.cpem.consumer

</td>
<td valign="top">

Receive messages from a queue in SAP BTP Enterprise Messaging and provide them for consumption in SAP Data Intelligence.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Integration](sap-integration-12600c5.md)

</td>
<td valign="top">

[SAP CP EM Producer](sap-cp-em-producer-6040d59.md)

</td>
<td valign="top">

com.sap.cpem.producer

</td>
<td valign="top">

Publish messages from SAP Data Intelligence to a topic in SAP BTP Enterprise Messaging.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Integration](sap-integration-12600c5.md)

</td>
<td valign="top">

[SAP CPI-PI iFlow](sap-cpi-pi-iflow-07fc1ed.md)

</td>
<td valign="top">

com.sap.cloud.cpi.pi

</td>
<td valign="top">

Provide the possibility to trigger iFlows in an SAP CPI system.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[ML Functional Services Inference \(Deprecated\)](ml-functional-services-inference-deprecated-b48efa5.md)

</td>
<td valign="top">

com.sap.ml.leonardo.MLFFunctionalServices

</td>
<td valign="top">

Prepare a request message for the Leonardo Machine Learning Foundation \(Leonardo MLF\) services.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="373be4daee074da38451a7339a8ec9a9.xml" text="" desc="" xtrc="xref:289" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

com.sap.ml.leonardo.objectDetectionInference

</td>
<td valign="top">

Prepare a request message for the Object Detection Inference service.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Functional Services \(Deprecated\)](functional-services-deprecated-64964b4.md)

</td>
<td valign="top">

com.sap.ml.functionalServices

</td>
<td valign="top">

Use ML pre-defined functional services.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Core Operators](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/aa92c9473ff14207929d4286e4769e45.html "This contains Modeler operators and Modeler graph templates that support core functions in SAP Data Intelligence.") :arrow_upper_right:

</td>
<td valign="top">

[Artifact Consumer](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/18e47f9018904e1aae5107364884e24b.html "Receives the id of a registered artifact and outputs its metadata. It is intended to be followed by an operator to retrieve the artifact file(s) from the Semantic Data Lake (SDL). For an example of usage of this operator, refer to the Python Consumer template pipeline.") :arrow_upper_right:

</td>
<td valign="top">

com.sap.ml.artifact.consumer

</td>
<td valign="top">

Retrieve and output a registered artifact.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Core Operators](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/aa92c9473ff14207929d4286e4769e45.html "This contains Modeler operators and Modeler graph templates that support core functions in SAP Data Intelligence.") :arrow_upper_right:

</td>
<td valign="top">

[Artifact Producer](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/9b8b01884a1e47c9a925e350fcc6b97f.html "The Artifact Producer operator registers the artifact (dataset, model or other) given as input and returns the artifact's generated ID.") :arrow_upper_right:

</td>
<td valign="top">

com.sap.ml.artifact.producer

</td>
<td valign="top">

Register the artifact given as input and return the artifact’s generated ID.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Core Operators](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/aa92c9473ff14207929d4286e4769e45.html "This contains Modeler operators and Modeler graph templates that support core functions in SAP Data Intelligence.") :arrow_upper_right:

</td>
<td valign="top">

[HANA ML Forecast](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/083780c468204924b286b6d595466d20.html "The HANA ML Forecast operator connects to an SAP HANA database and leverages algorithms from SAP HANA Predictive Analytics Library (PAL) or SAP HANA Automated Predictive Library (APL) that do not require a model to be persisted. Instead, the model is generated on-the-fly based on the input data, and a series of results are then forecast automatically.") :arrow_upper_right:

</td>
<td valign="top">

com.sap.ml.hana.forecast

</td>
<td valign="top">

Connect to an SAP HANA database and leverages algorithms from SAP HANA Predictive Analytics Library \(PAL\) or SAP HANA Automated Predictive Library \(APL\) that do not require a model to be persisted.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Core Operators](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/aa92c9473ff14207929d4286e4769e45.html "This contains Modeler operators and Modeler graph templates that support core functions in SAP Data Intelligence.") :arrow_upper_right:

</td>
<td valign="top">

[HANA ML Inference](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/3177cdaea9af4809bb00a0f2da972cdc.html "Connects to a SAP HANA database instance and applies the specified machine learning model, leveraging SAP HANA Predictive Analytics Library (PAL) or SAP HANA Automated Predictive Library (APL). The input data for inference is supplied either from a table in the SAP HANA database (using the Inference Dataset parameter) or via the inferenceData input port. In case both are supplied, only data from the Inference Dataset parameter is processed.") :arrow_upper_right:

</td>
<td valign="top">

com.sap.ml.hana.inference

</td>
<td valign="top">

Connect to a HANA database and apply the specified trained Machine Learning model leveraging SAP HAJA Predictive Analytics Library \(PAL\).

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Core Operators](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/aa92c9473ff14207929d4286e4769e45.html "This contains Modeler operators and Modeler graph templates that support core functions in SAP Data Intelligence.") :arrow_upper_right:

</td>
<td valign="top">

[HANA ML Training](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/cebdb4bbaa444b6ab6bbfde76e2810e9.html "Connects to a SAP HANA database and generates a machine learning model using the specified algorithm leveraged by SAP HANA Predictive Analytics Library (PAL) or SAP HANA Automated Predictive Library (APL). In case of successful execution, it outputs the generated model and its associated metrics (if a test dataset is provided or dataset is split into training/testing).") :arrow_upper_right:

</td>
<td valign="top">

com.sap.ml.hana.training

</td>
<td valign="top">

Connect to a SAP HANA database and generate a Machine Learning model using the specified algorithm leveraged by SAP HANA Predictive Analytics Library \(PAL\).

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Core Operators](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/aa92c9473ff14207929d4286e4769e45.html "This contains Modeler operators and Modeler graph templates that support core functions in SAP Data Intelligence.") :arrow_upper_right:

</td>
<td valign="top">

[ML Training](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/702bee29ce7c4f3497262221d4145b7a.html "Use this operator to run a Machine Learning training script. This operator runs on Python 3.9.") :arrow_upper_right:

</td>
<td valign="top">

com.sap.ml.training.v2

</td>
<td valign="top">

Run a Machine Learning training script.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Core Operators](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/aa92c9473ff14207929d4286e4769e45.html "This contains Modeler operators and Modeler graph templates that support core functions in SAP Data Intelligence.") :arrow_upper_right:

</td>
<td valign="top">

[Model Serving](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/590ccd20ab214e499dfc6ce4591c6430.html "The Model Serving operator deploys Machine Learning (ML) models and handles inference request for the deployed models.") :arrow_upper_right:

</td>
<td valign="top">

com.sap.ml.modelServingOperator

</td>
<td valign="top">

Deploy a Machine Learning \(ML\) model and handle inference requests for the model.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Core Operators](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/aa92c9473ff14207929d4286e4769e45.html "This contains Modeler operators and Modeler graph templates that support core functions in SAP Data Intelligence.") :arrow_upper_right:

</td>
<td valign="top">

[Submit Metrics](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/b792d72b009a41b090c896d374a4dc17.html "The Submit Metrics operator submits your model metrics to the ML Tracking API. The metrics can be viewed in ML Scenario Manager.") :arrow_upper_right:

</td>
<td valign="top">

com.sap.ml.submitMetrics

</td>
<td valign="top">

Submit your model metrics to the ML Tracking API. The metrics can be viewed in ML Scenario Manager.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Functional Services](sap-machine-learning-functional-services-357beb4.md)

</td>
<td valign="top">

[Image Classification](image-classification-9c2e589.md)

</td>
<td valign="top">

com.sap.ml.fs.image\_classification

</td>
<td valign="top">

Classify one image at each step.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Functional Services](sap-machine-learning-functional-services-357beb4.md)

</td>
<td valign="top">

[Image Feature Extraction](image-feature-extraction-c964cda.md)

</td>
<td valign="top">

com.sap.ml.fs.image\_feature\_extraction

</td>
<td valign="top">

Extract one vector at each step.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Functional Services](sap-machine-learning-functional-services-357beb4.md)

</td>
<td valign="top">

[OCR](ocr-47a163e.md)

</td>
<td valign="top">

com.sap.ml.fs.ocr

</td>
<td valign="top">

Classify one image or a PDF with multiple pages at each step.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Functional Services](sap-machine-learning-functional-services-357beb4.md)

</td>
<td valign="top">

[Similarity Score](similarity-score-392e0b8.md)

</td>
<td valign="top">

com.sap.ml.fs.similarity\_scoring

</td>
<td valign="top">

Calculate the similarity between two images.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Functional Services](sap-machine-learning-functional-services-357beb4.md)

</td>
<td valign="top">

[Text Classification](text-classification-21c882a.md)

</td>
<td valign="top">

com.sap.ml.fs.text\_classification

</td>
<td valign="top">

Classify one input at each step and receive a string as input.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Machine Learning Functional Services](sap-machine-learning-functional-services-357beb4.md)

</td>
<td valign="top">

[Topic Detection](topic-detection-df20169.md)

</td>
<td valign="top">

com.sap.ml.fs.topic\_detection

</td>
<td valign="top">

Predict the topics among the text document samples.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[Avro Decoder](avro-decoder-1509d8f.md)

</td>
<td valign="top">

com.sap.vora.preingestor

</td>
<td valign="top">

Decode messages represented in various formats such as Avro, CSV, and JSON for processing in the pipeline.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[Avro Encoder](avro-encoder-1676e87.md)

</td>
<td valign="top">

com.sap.vora.postassembler

</td>
<td valign="top">

Create Avro, CSV, or JSON messages from messages containing record objects.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Structured Data Operators](structured-data-operators-e99abce.md)

</td>
<td valign="top">

-   [Data Transform](data-transform-4d9d1f2.md)
-   [Data Transform V2](data-transform-v2-a415f61.md)



</td>
<td valign="top">

-   com.sap.datatransform
-   com.sap.datatransform.v2



</td>
<td valign="top">

Provide wide variety of options to meet your data transformation needs.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Structured Data Operators](structured-data-operators-e99abce.md)

</td>
<td valign="top">

-   [SAP Application Consumer](sap-application-consumer-7c8efaa.md)
-   [SAP Application Consumer V2](sap-application-consumer-v2-7a1527d.md)



</td>
<td valign="top">

-   com.sap.application.consumer.v2
-   com.sap.application.consumer.v3



</td>
<td valign="top">

Read from a variety of SAP and non-SAP applications, and produce structured output.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Structured Data Operators](structured-data-operators-e99abce.md)

</td>
<td valign="top">

-   [SAP Application Producer](sap-application-producer-671cf97.md)
-   [SAP Application Producer V2](sap-application-producer-v2-c8095cf.md)



</td>
<td valign="top">

-   com.sap.application.producer
-   com.sap.application.producer.v2



</td>
<td valign="top">

Read from any structured operators, and produce a table in the specified target like oData and BW.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Structured Data Operators](structured-data-operators-e99abce.md)

</td>
<td valign="top">

-   [SQL Consumer](sql-consumer-2ecef35.md)
-   [SQL Consumer V2](sql-consumer-v2-a4a74c3.md)



</td>
<td valign="top">

-   com.sap.database.sql.consumer
-   com.sap.database.sql.consumer.v3



</td>
<td valign="top">

Read from a specified database using native SQL.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Structured Data Operators](structured-data-operators-e99abce.md)

</td>
<td valign="top">

-   [Structured File Consumer V2](structured-file-consumer-v2-8dc5832.md)
-   [Structured File Consumer V3](structured-file-consumer-v3-02d49cc.md)



</td>
<td valign="top">

-   com.sap.storage.consumer
-   com.sap.storage.consumer.v3



</td>
<td valign="top">

Read from any cloud storage.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Structured Data Operators](structured-data-operators-e99abce.md)

</td>
<td valign="top">

-   [Structured File Producer V2](structured-file-producer-v2-aa3dbf1.md)
-   [Structured File Producer V3](structured-file-producer-v3-605e08a.md)



</td>
<td valign="top">

-   com.sap.storage.producer
-   com.sap.storage.producer.v3



</td>
<td valign="top">

Read from any structured data operators and produce a file \(CSV, ORC, or PARQUET\) in the specified storage.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Structured Data Operators](structured-data-operators-e99abce.md)

</td>
<td valign="top">

-   [Table Consumer](table-consumer-bfb3966.md)
-   [Table Consumer V2](table-consumer-v2-1e5f0ee.md)



</td>
<td valign="top">

-   com.sap.database.table.consumer
-   com.sap.database.table.consumer.v3



</td>
<td valign="top">

Read from an specified database table or view, and produce a structured output.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Structured Data Operators](structured-data-operators-e99abce.md)

</td>
<td valign="top">

-   [Table Producer V2](table-producer-v2-acd8dbe.md)
-   [Table Producer V3](table-producer-v3-092de44.md)



</td>
<td valign="top">

-   com.sap.database.table.producer
-   com.sap.database.table.producer.v3



</td>
<td valign="top">

Read from any structured operators, and produce a table in the specified database.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Structured Data Operators](structured-data-operators-e99abce.md)

</td>
<td valign="top">

[Table to Message Converter](table-to-message-converter-03705cd.md)

</td>
<td valign="top">

com.sap.util.tableToMessageConverter

</td>
<td valign="top">

Receive a vType as input and then output the data as message content with a CSV body as a string.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[Application Logging](application-logging-5e009c4.md)

</td>
<td valign="top">

com.sap.dh.applogging

</td>
<td valign="top">

Write application messages as logs through the application logging API.

</td>
<td valign="top">

 

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[Decode Table](decode-table-a40bf41.md)

</td>
<td valign="top">

com.sap.table.decode

</td>
<td valign="top">

Decode tabular data from one of the supported formats into table messages.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="e9b1ec9150564a36b77c3844e611c8f3.xml" text="" desc="" xtrc="xref:363" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

com.sap.util.headerRemover

</td>
<td valign="top">

Remove specified headers from a message.

</td>
<td valign="top">

 

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="ec31762cfe8c4da18ef8cbb2707a3092.xml" text="" desc="" xtrc="xref:365" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

com.sap.textanalysis.taconnector

</td>
<td valign="top">

Connect to a text analysis server using an external connector binary.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [https://me.sap.com/notes/](https://me.sap.com/notes/https://me.sap.com/notes/)[2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="8adb1b8226fb40dfb5c8e35329aa9a2e.xml" text="" desc="" xtrc="xref:366" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

[Binary to Table V2](binary-to-table-v2-1bb16c0.md)

</td>
<td valign="top">

com.sap.table.decode.v2

</td>
<td valign="top">

Decode serialized data and provide the data in table format.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="8adb1b8226fb40dfb5c8e35329aa9a2e.xml" text="" desc="" xtrc="xref:368" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

[Generate Table](generate-table-76055ab.md)

</td>
<td valign="top">

com.sap.table.generate

</td>
<td valign="top">

Generate Table Messages with a user-defined schema and random data.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="8adb1b8226fb40dfb5c8e35329aa9a2e.xml" text="" desc="" xtrc="xref:370" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

[Table to Binary](table-to-binary-f0ba7fa.md)

</td>
<td valign="top">

com.sap.table.encode

</td>
<td valign="top">

Encode table data in a serialization data format.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Avro Serializer \(Deprecated\)](avro-serializer-deprecated-f0abafa.md)

</td>
<td valign="top">

com.sap.util.avroSerializer

</td>
<td valign="top">

Convert CSV encoded lines and produce the contents as Avro encoded messages.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Avro Deserializer \(Deprecated\)](avro-deserializer-deprecated-c265c32.md)

</td>
<td valign="top">

com.sap.util.avroDeserializer

</td>
<td valign="top">

Convert Avro-encoded messages and produce the contents as CSV-encoded lines.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Flowgraph Compiler \(Deprecated\)](flowgraph-compiler-deprecated-1760e52.md)

</td>
<td valign="top">

com.sap.bdh.flowgraphCompiler

</td>
<td valign="top">

Compile incoming flowgraph XML strings into jars, which can be executed via Spark.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[Format Converter](format-converter-c5b81c7.md)

</td>
<td valign="top">

com.sap.util.formatConverter

</td>
<td valign="top">

Convert blobs between CSV, JSON, and XML.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

-   [Graph Terminator](graph-terminator-26f7ff3.md)

-   [Graph Terminator V2](graph-terminator-v2-190cbc7.md)



</td>
<td valign="top">

-   com.sap.util.graphTerminator

-   com.sap.util.graphTerminator.v2



</td>
<td valign="top">

Terminate the current graph execution.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[Histogram](histogram-814a342.md)

</td>
<td valign="top">

com.sap.util.histogram

</td>
<td valign="top">

Receive a numeric value as input and increment the counter of the bin that corresponds to the range in which the value lies.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[Histogram Plotter](histogram-plotter-d9222a6.md)

</td>
<td valign="top">

com.sap.util.histogramPlotter

</td>
<td valign="top">

Receive a string-converted Modeler message as input with an array of integers in the body and rangeMin and rangeMax fields in the header.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[HTML Viewer](html-viewer-1fa7e90.md)

</td>
<td valign="top">

com.sap.util.htmlViewer

</td>
<td valign="top">

Render HTML code on the browser as it arrives at the input port.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[Message Aggregator](message-aggregator-7957539.md)

</td>
<td valign="top">

com.sap.util.aggregator

</td>
<td valign="top">

Aggregate input messages in a custom manner specified by JavaScript functions that you can enter.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

-   [Py3 Data Generator](py3-data-generator-062fd1d.md)
-   [Py3 Data Generator V2](py3-data-generator-v2-236f940.md)



</td>
<td valign="top">

-   com.sap.util.datageneratorpy3
-   com.sap.util.datageneratorpy3.v2



</td>
<td valign="top">

Generate random sample data every 500ms.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[Py3 Type to Blob](py3-type-to-blob-ff0a160.md)

</td>
<td valign="top">

com.sap.util.python3TypeToBlob

</td>
<td valign="top">

Serialize any Python3 data received in its input port and send the result to the output port.

</td>
<td valign="top">

Actibe

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

[Py3 Type to String](py3-type-to-string-f723d84.md)

</td>
<td valign="top">

com.sap.util.python3TypeToString

</td>
<td valign="top">

Convert any Python 3 data received in its input to string by feeding it into the standard Python str\(.\) function.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

-   [Terminal](terminal-2f28daf.md)

-   [Terminal V2](terminal-v2-b8522e3.md)



</td>
<td valign="top">

-   com.sap.util.terminal

-   com.sap.util.terminal.v2



</td>
<td valign="top">

Represent a terminal window in the browser.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Utilities](utilities-7beeaa8.md)

</td>
<td valign="top">

-   [Wiretap](wiretap-2a0c233.md)

-   [Wiretap V2](wiretap-v2-6330e23.md)



</td>
<td valign="top">

-   com.sap.util.wiretap

-   com.sap.util.wiretap.v2



</td>
<td valign="top">

Wiretap a connection between two operators in a Pipeline Engine graph and display the traffic to the browser window or to an external WebSocket client that connects to this operator.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Blob Consumer \(Deprecated\)](blob-consumer-deprecated-5f546d0.md)

</td>
<td valign="top">

com.sap.blob.consumer

</td>
<td valign="top">

Consume a blob in the blob repository.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[Blob Producer \(Deprecated\)](blob-producer-deprecated-12e7580.md)

</td>
<td valign="top">

com.sap.blob.producer

</td>
<td valign="top">

Push a blob to the blob repository.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

[SAP ABAP ODP Object Consumer \(Deprecated\)](sap-abap-odp-object-consumer-deprecated-74fb553.md)

</td>
<td valign="top">

com.sap.dh.ds.abap.odp.consumer

</td>
<td valign="top">

Use Flowagent for execution.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

[ABAP ODP Reader](abap-odp-reader-d4c18f8.md)

com.sap.abap.odp.read

</td>
</tr>
<tr>
<td valign="top">

[Deprecated Operators](deprecated-operators-dd8043a.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="1e5416945af842d196bea40e3ebc702b.xml" text="" desc="" xtrc="xref:416" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/acd32810819a4b2893c9f8698e2ec55c.xml" ?> 

</td>
<td valign="top">

com.sap.textanalysis.tarequestcreator

</td>
<td valign="top">

Create a request for the Text Analysis Connector operator in JSON format.

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

See SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.

</td>
</tr>
<tr>
<td valign="top">

[Multiplexer](multiplexer-84c572a.md)

</td>
<td valign="top">

[Multiplexer](multiplexer-84c572a.md)

</td>
<td valign="top">

-   com.sap.system.multiplexer.1-10
-   com.sap.system.multiplexer.1-2
-   com.sap.system.multiplexer.1-3
-   com.sap.system.multiplexer.1-4
-   com.sap.system.multiplexer.1-5
-   com.sap.system.multiplexer.10-1
-   com.sap.system.multiplexer.2-1
-   com.sap.system.multiplexer.3-1
-   com.sap.system.multiplexer.4-1
-   com.sap.system.multiplexer.5-1



</td>
<td valign="top">

Map the input of any port to all of its output ports.

</td>
<td valign="top">

Active

</td>
<td valign="top">

 

</td>
</tr>
</table>

-   **[Generation 1](generation-1-30ba378.md "")**  

-   **[Generation 2](generation-2-aba671a.md "")**  

-   **[Partitioning](partitioning-86085d9.md "Data partitioning separates large datasets into smaller ones based on a set of defined criteria. ")**  
Data partitioning separates large datasets into smaller ones based on a set of defined criteria.
-   **[Deprecated Operators](deprecated-operators-dd8043a.md "Operators that will be removed from the software are listed as Deprecated.
		In most cases, an alternate operator is recommended. ")**  
Operators that will be removed from the software are listed as *Deprecated*. In most cases, an alternate operator is recommended.

