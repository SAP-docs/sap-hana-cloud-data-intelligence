<!-- loioa25fe767e51e4c5b8c2eb09d24a7bff4 -->

# SAP Data Intelligence Graphs

A graph is a network of operators connected to each other using typed input ports and output ports for data transfer. Users can define and configure the operators in a graph.

For information about using SAP Data Intelligence `graphs` and creating your own custom graphs, see [Creating Graphs](https://help.sap.com/viewer/1c1341f6911f4da5a35b191b40b426c8/Cloud/en-US/aea42f8cf13740f8af59b8cb89939147.html "A graph (pipeline) consists of operators that you configure to form a specific process and connect using input and output ports.") :arrow_upper_right: in the *Modeling Guide for SAP Data Intelligence*.

****


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Graph

</th>
<th valign="top">

Technical Name

</th>
<th valign="top">

Primary Use Case

</th>
<th valign="top">

Status

</th>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-4cfe81e.md)

</td>
<td valign="top">

[Example for OpenAPI Greeter Demo \(Go\)](example-for-openapi-greeter-demo-go-c08c790.md)

</td>
<td valign="top">

com.sap.demo.openapi.server.greeter\_go

</td>
<td valign="top">

Allow REST services to be exposed from a graph.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-4cfe81e.md)

</td>
<td valign="top">

[Example for OpenAPI Plain Greeter Demo \(Go\)](example-for-openapi-plain-greeter-demo-go-10a08cc.md)

</td>
<td valign="top">

com.sap.demo.openapi.server.plain\_greeter\_go

</td>
<td valign="top">

Allow REST services to be exposed from a graph.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-4cfe81e.md)

</td>
<td valign="top">

[Google Pub/Sub](google-pub-sub-94ab34d.md)

</td>
<td valign="top">

com.sap.demo.googlepubsub

</td>
<td valign="top">

Publish messages using the Google Pub/Sub Producer, and consume them via the Google Pub/Sub Consumer.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-4cfe81e.md)

</td>
<td valign="top">

[Kafka](kafka-991d1bc.md)

</td>
<td valign="top">

com.sap.demo.kafka

</td>
<td valign="top">

Generate arbitrary data and pass it to the Kafka producer. The Kafka consumer reads the data and writes it to a terminal.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-4cfe81e.md)

</td>
<td valign="top">

[OpenAPI GreeterClient Demo](openapi-greeterclient-demo-9c3954b.md)

</td>
<td valign="top">

com.sap.demo.openapi.client.greeter

</td>
<td valign="top">

Call arbitrary REST services from a graph.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-4cfe81e.md)

</td>
<td valign="top">

[OpenAPI PlainClient Demo](openapi-plainclient-demo-c436390.md)

</td>
<td valign="top">

com.sap.demo.openapi.client.plain\_greeter

</td>
<td valign="top">

Call arbitrary REST services from a graph.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-4cfe81e.md)

</td>
<td valign="top">

[OpenAPI Greeter Demo](openapi-greeter-demo-f4310e5.md)

</td>
<td valign="top">

com.sap.demo.openapi.server.greeter

</td>
<td valign="top">

Expose REST services from a graph.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-4cfe81e.md)

</td>
<td valign="top">

[OpenAPI Plain Greeter](openapi-plain-greeter-54d279d.md)

</td>
<td valign="top">

com.sap.demo.openapi.server.plain\_greeter

</td>
<td valign="top">

Expose REST services from a graph.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-4cfe81e.md)

</td>
<td valign="top">

[OpenAPI Middleware Demo](openapi-middleware-demo-575cd07.md)

</td>
<td valign="top">

com.sap.demo.openapi.middleware.greeter

</td>
<td valign="top">

Eeceive REST requests at its own service path and forward the requests to the greeter demo graph’s service path in order to invoke the corresponding greeter service operations.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Connectivity](connectivity-4cfe81e.md)

</td>
<td valign="top">

[S3](s3-25f01ef.md)

</td>
<td valign="top">

com.sap.demo.s3

</td>
<td valign="top">

Produce arbitrary data from the data generator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Anonymization](anonymization-eee0a03.md)

</td>
<td valign="top">

com.sap.demo.anonymization2

</td>
<td valign="top">

Protect the privacy of individuals by creating groups of similar records.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Basic Validation Rule](basic-validation-rule-3e1b0c7.md)

</td>
<td valign="top">

com.sap.demo.validationRule.basicValidationRule

</td>
<td valign="top">

Evaluate input data against a rule.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Data Generator](data-generator-cb7028b.md)

</td>
<td valign="top">

com.sap.demo.datagenerator

</td>
<td valign="top">

Generate arbitrary values from the data generator simulating a set of sensors.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Data Mask](data-mask-625e5df.md)

</td>
<td valign="top">

com.sap.demo.dataMask

</td>
<td valign="top">

Protect the personally identifiable or sensitive information by covering all or a portion of the data.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples](examples-ff56220.md)

</td>
<td valign="top">

[Data Workflow](data-workflow-2714f1e.md)

</td>
<td valign="top">

com.sap.demo.dataworkflow

</td>
<td valign="top">

Start an internal example graph. It serves as an example on how to use the operators from the Data Workflow category.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[DQMm Address Cleanse](dqmm-address-cleanse-7eb9478.md)

</td>
<td valign="top">

com.sap.demo.dqmm.addrCleanse

</td>
<td valign="top">

Create a request from data that can be passed to the DQMm Client operator to be sent to the service.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[DQMm Reverse Geo](dqmm-reverse-geo-5335ef1.md)

</td>
<td valign="top">

com.sap.demo.dqmm.reverseGeo

</td>
<td valign="top">

Creates a request from data that can be passed to the DQMm Client operator to be sent to the service.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples](examples-ff56220.md)

</td>
<td valign="top">

[Example Counter](example-counter-1f08e7c.md)

</td>
<td valign="top">

com.sap.demo.counter

</td>
<td valign="top">

Run tests with this graph, which runs for five seconds and then shuts down with status “completed”.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples](examples-ff56220.md)

</td>
<td valign="top">

[Example Notification](example-notification-3fe55dd.md)

</td>
<td valign="top">

com.sap.demo.notification

</td>
<td valign="top">

Use SAP Data Intelligence Notification and Pipeline operators from the Data Workflows category.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[File System](file-system-170742e.md)

</td>
<td valign="top">

com.sap.demo.file

</td>
<td valign="top">

Generate arbitrary data from the data generator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Go Data Generator](go-data-generator-20a10c8.md)

</td>
<td valign="top">

com.sap.demo.goDataGenerator

</td>
<td valign="top">

Generate arbitrary values from the data generator simulating a set of sensors.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Go Message Generator](go-message-generator-6ed1d0a.md)

</td>
<td valign="top">

com.sap.demo.goMessageGenerator

</td>
<td valign="top">

Generate arbitrary values packed into a message, simulating a set of sensors.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Go Operator and File Reader](go-operator-and-file-reader-775e229.md)

</td>
<td valign="top">

com.sap.demo.system.goOperator

</td>
<td valign="top">

Read content from a file, and use Go Operator in order to deal with the file content and name, using different Go functions and message type in Go Operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples](examples-ff56220.md)

</td>
<td valign="top">

[Go Plugin Generator](go-plugin-generator-287a595.md)

</td>
<td valign="top">

com.sap.demo.system.goplugingen

</td>
<td valign="top">

Build the compatible plugin libraries for a graph that contains Go programs with external package dependencies.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Simple Command Executor](simple-command-executor-3407cb7.md)

</td>
<td valign="top">

com.sap.demo.commandExecutor

</td>
<td valign="top">

Execute a build-in Unix command on the input and pipe the result to the output port `stdout`.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples](examples-ff56220.md)

</td>
<td valign="top">

[Google Dataproc](google-dataproc-7b273c1.md)

</td>
<td valign="top">

com.sap.demo.hadoop.dataproc

</td>
<td valign="top">

Submit a Spark job to an existing Google Dataproc cluster, and see the results of the job.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[HTML Viewer](html-viewer-ec75129.md)

</td>
<td valign="top">

com.sap.demo.htmlViewer

</td>
<td valign="top">

Simulate a Sales Campaign generating pseudorandom data for a large number of stores.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Histogram Simple Example](histogram-simple-example-805f652.md)

</td>
<td valign="top">

com.sap.demo.util.histogramSimple

</td>
<td valign="top">

Generate random numbers that are sent to the Histogram operator, which produces the histogram of its inputs as a Message, with an integer array on its body, and the range of the interval on its attributes.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[IoT Validation Rule](iot-validation-rule-4e28c23.md)

</td>
<td valign="top">

com.sap.demo.validationRule.IoTValidationRule

</td>
<td valign="top">

Model a sensor that tracks the temperature and surface illuminance of ice cream.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples](examples-ff56220.md)

</td>
<td valign="top">

[Jupyter Example](jupyter-example-61af45d.md)

</td>
<td valign="top">

com.sap.demo.jupyter

</td>
<td valign="top">

Illustrate how a Jupyter operator can be used to interact with data flowing through the graph.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Kafka](kafka-31675b8.md)

</td>
<td valign="top">

com.sap.demo.kafka

</td>
<td valign="top">

Generates arbitrary data and passes it to the Kafka producer.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="9710156f82834c10a496e4bc939ab34c.xml" text="" desc="" xtrc="xref:64" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[Load into SAP HANA](load-into-sap-hana-d57498a.md)

</td>
<td valign="top">

com.sap.demo.hana

</td>
<td valign="top">

Produce sensor data as a CSV string. The data is loaded into SAP HANA and in parallel sent to a terminal.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Message Generator](message-generator-8e326df.md)

</td>
<td valign="top">

com.sap.demo.messageGenerator

</td>
<td valign="top">

Generate arbitrary values packed into a message, simulating a set of sensors.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Person and Firm Cleanse](person-and-firm-cleanse-c519383.md)

</td>
<td valign="top">

com.sap.demo.personAndFirmCleanse

</td>
<td valign="top">

Parse and standardize person and firm \(business organization\) data.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples](examples-ff56220.md)

</td>
<td valign="top">

[RClient Example](rclient-example-a491bc0.md)

</td>
<td valign="top">

com.sap.demo.rClientExample

</td>
<td valign="top">

Show the different features of the RClient operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md)

</td>
<td valign="top">

[Simple Wiring](simple-wiring-682921b.md)

</td>
<td valign="top">

com.sap.demo.others.simple-wiring

</td>
<td valign="top">

Connect three data generating operators of different output port types to a wiretap, that is directly connected to a terminal and another wiretap.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Examples](examples-ff56220.md)[Examples](examples-ff56220.md)

</td>
<td valign="top">

[S3](s3-c15b8e1.md)

</td>
<td valign="top">

com.sap.demo.s3

</td>
<td valign="top">

Generate arbitrary data from the data generator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="9710156f82834c10a496e4bc939ab34c.xml" text="" desc="" xtrc="xref:77" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[Binary to Table Example](binary-to-table-example-3c2f3b5.md)

</td>
<td valign="top">

com.sap.demo.table.decode

</td>
<td valign="top">

Read a file with input data in CSV format and convert the file contents to vtype table format.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="9710156f82834c10a496e4bc939ab34c.xml" text="" desc="" xtrc="xref:79" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[Table to Binary Example](table-to-binary-example-59faafb.md)

</td>
<td valign="top">

com.sap.demo.table.encode

</td>
<td valign="top">

Take generated input in vtype table format and convert the data to CSV format.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:81" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[HANA to File](hana-to-file-866afc2.md)

</td>
<td valign="top">

com.sap.generation2Examples.scenario.hanaToFile

</td>
<td valign="top">

Showcase how to read a table from a HANA database, modify it, and write to a partitioned file on a remote file system in the CSV format

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:83" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[HANA to HANA](hana-to-hana-47178dd.md)

</td>
<td valign="top">

com.sap.generation2Examples.scenario.hanaToHana

</td>
<td valign="top">

Showcase how to read one HANA database table and write to another.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:85" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[HANA to Kafka](hana-to-kafka-7d04ad8.md)

</td>
<td valign="top">

com.sap.generation2Examples.scenario.hanaToKafka

</td>
<td valign="top">

Showcase how to read a HANA database table and write the data into a Kafka server.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:87" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[Kafka to HANA](kafka-to-hana-bbb754a.md)

</td>
<td valign="top">

com.sap.generation2Examples.scenario.kafkaToHana

</td>
<td valign="top">

Showcase how to read from a Kafka server topic and write the data into a HANA database table.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:89" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[SQL to File](sql-to-file-5bbb577.md)

</td>
<td valign="top">

com.sap.generation2Examples.scenario.sqlToFile

</td>
<td valign="top">

Showcase how to run a single or multiple Select statements and write the result set\(s\) to a partitioned file on a remote file system in the CSV format.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:91" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[Multiplexer for Dynamic Inputs](multiplexer-for-dynamic-inputs-c452e2f.md)

</td>
<td valign="top">

com.sap.generation2Examples.demo.multiplexerForDynamicInputs

</td>
<td valign="top">

Showcase how to read dynamic data from more than one input and write to one output using a Python Operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:93" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[Multiplexer for Dynamic Outputs](multiplexer-for-dynamic-outputs-36cf758.md)

</td>
<td valign="top">

com.sap.generation2Examples.demo.multiplexerForDynamicOutputs

</td>
<td valign="top">

Showcase how to read dynamic data from an input and write to multiple outputs using a Python Operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:95" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[Multiplexer for Static Inputs](multiplexer-for-static-inputs-7b17827.md)

</td>
<td valign="top">

com.sap.generation2Examples.demo.multiplexerForStaticInputs

</td>
<td valign="top">

Showcase how to read static data from more than one input and write to one output using a Python Operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:97" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[Multiplexer for Static Outputs](multiplexer-for-static-outputs-bba574e.md)

</td>
<td valign="top">

com.sap.generation2Examples.demo.multiplexerForStaticOutputs

</td>
<td valign="top">

Showcase how to read static data from an input and write to multiple outputs using a Python Operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:99" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[Static to Dynamic Converter](static-to-dynamic-converter-0f4bf34.md)

</td>
<td valign="top">

com.sap.generation2Examples.demo.staticToDynamicConverter

</td>
<td valign="top">

Showcase how to read data from an input with static data type and write into an output with dynamic data type using a Python Operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="50a5b58582e84d11991eb5f14a89d107.xml" text="" desc="" xtrc="xref:101" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

[Dynamic to Static Converter](dynamic-to-static-converter-90981f9.md)

</td>
<td valign="top">

com.sap.generation2Examples.demo.dynamicToStaticConverter

</td>
<td valign="top">

Showcase how to read data from an input with dynamic data type and write into an output with static data type using a Python Operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

[Data Extraction from SAP ABAP Table to a File Store via SLT](data-extraction-from-sap-abap-table-to-a-file-store-via-slt-b1690cb.md)

</td>
<td valign="top">

com.sap.abap.SLTtoFile

</td>
<td valign="top">

Extract data from an SAP ABAP table via SAP Landscape Transformation Replication Server \(SLT\) to a file store and create related files in the file store.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

[Data Extraction from SAP ABAP Table to Kafka via SLT](data-extraction-from-sap-abap-table-to-kafka-via-slt-33c412a.md)

</td>
<td valign="top">

com.sap.abap.SLTtoKafka

</td>
<td valign="top">

Extract data from an SAP ABAP table via SAP Landscape Transformation Replication Server \(SLT\) to a Kafka-Broker.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

[Data Extraction from SAP S/4HANA CDS View to a File Store](data-extraction-from-sap-s-4hana-cds-view-to-a-file-store-f8bc312.md)

</td>
<td valign="top">

com.sap.abap.CDStoFile

</td>
<td valign="top">

Extract data from an ABAP CDS View to a file store and create related files in the file store.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

[Data Extraction from SAP S/4HANA CDS View to Kafka](data-extraction-from-sap-s-4hana-cds-view-to-kafka-54e91eb.md)

</td>
<td valign="top">

com.sap.abap.CDStoKafka

</td>
<td valign="top">

Extract data from an ABAP CDS View to a Kafka-Broker.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

[Simple Javascript DB-to-File Data Manipulation](simple-javascript-db-to-file-data-manipulation-7ae76bf.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleDB2FJavascript

</td>
<td valign="top">

Manipulate data from an SAP HANA database table using plain Javascript \(ECMAScript 2009 / ES5\) and writing the manipulated data to a file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="1b568d8e037b43f9be93b31e8653d355.xml" text="" desc="" xtrc="xref:114" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2FJavascript

</td>
<td valign="top">

Exemplify file data manipulation using plain Javascript \(without any libraries\) and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

[Simple Javascript File-to-DB Data Manipulation](simple-javascript-file-to-db-data-manipulation-740d761.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2DBJavascript

</td>
<td valign="top">

Manipulate data using plain Javascript \(without any libraries\) and write the manipulated data to an SAP HANA database table.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="c662addd2a8447f2914a8ff68b8850e8.xml" text="" desc="" xtrc="xref:118" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2FNode

</td>
<td valign="top">

Exemplify file data manipulation using Node.js \(without any libraries\) and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

[Simple Python File Data Manipulation](simple-python-file-data-manipulation-5337682.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2FPython

</td>
<td valign="top">

Exemplify file data manipulation using plain Python with only built-in modules and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="0e3a8cca95f441a9b92451770568c189.xml" text="" desc="" xtrc="xref:122" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2DBPython

</td>
<td valign="top">

Manipulate data using plain Python and write the manipulated data to an SAP HANA database table.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

[Simple R File Data Manipulation](simple-r-file-data-manipulation-ac09193.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2FR

</td>
<td valign="top">

Exemplify file data manipulation using plain R \(using only built-in libraries\) and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Graph Snippets](graph-snippets-46542f8.md)

</td>
<td valign="top">

[Simple R File-to-DB Data Manipulation](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/46d882a1c4704518a4ea94ddb9fefd00.html "File data manipulation using plain R (using only built-in libraries) and writing the manipulated data to an SAP HANA database table.") :arrow_upper_right:

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2DBR

</td>
<td valign="top">

Manipulate data using plain R \(using only built-in libraries\) and write the manipulated data to an SAP HANA database table.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Ingestion via Flowagent](ingestion-via-flowagent-139b202.md)

</td>
<td valign="top">

[CSV Producer](csv-producer-055bdbd.md)

</td>
<td valign="top">

com.sap.dh.ingestion.csvproducer

</td>
<td valign="top">

Use the CSV Producer operator mainly to detail the usability of the outMessage port.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Ingestion via Flowagent](ingestion-via-flowagent-139b202.md)

</td>
<td valign="top">

[Ingest OData Query](ingest-odata-query-45049ee.md)

</td>
<td valign="top">

com.sap.dh.ingestion.odata.queryconsumer

</td>
<td valign="top">

Read data from an API, which implements the protocol.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Ingestion via Flowagent](ingestion-via-flowagent-139b202.md)

</td>
<td valign="top">

[Ingest Google BigQuery SQL](ingest-google-bigquery-sql-bf0b98f.md)

</td>
<td valign="top">

com.sap.dh.ingestion.gbq.sqlconsumer

</td>
<td valign="top">

Demonstrate how to use Google BigQuery SQL Consumer.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Ingestion via Flowagent](ingestion-via-flowagent-139b202.md)

</td>
<td valign="top">

[Ingest Google BigQuery Table Producer](ingest-google-bigquery-table-producer-734a58a.md)

</td>
<td valign="top">

com.sap.dh.ingestion.gbq.producer

</td>
<td valign="top">

Demonstrate how to use the Google BiQuery Table Producer.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Ingestion via Flowagent](ingestion-via-flowagent-139b202.md)

</td>
<td valign="top">

[Open Connectors SQL Consumer](open-connectors-sql-consumer-52365da.md)

</td>
<td valign="top">

com.sap.dh.ingestion.openconnectors.sqlconsumer

</td>
<td valign="top">

See how to use Open Connectors SQL Consumer, which is a Flowagent operator and uses Flowagent subengine for execution.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Ingestion via Flowagent](ingestion-via-flowagent-139b202.md)

</td>
<td valign="top">

[Open Connectors Table Consumer](open-connectors-table-consumer-b8b52d2.md)

</td>
<td valign="top">

com.sap.dh.ingestion.openconnectors.tableconsumer

</td>
<td valign="top">

Use Open Connectors Table Consumer, which is a Flowagent operator that uses Flowagent sub engine for execution.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Ingestion via Flowagent](ingestion-via-flowagent-139b202.md)

</td>
<td valign="top">

[Ingest to a Table via Flowagent](ingest-to-a-table-via-flowagent-c0aa224.md)

</td>
<td valign="top">

com.sap.dh.ingestion.tableconsumer

</td>
<td valign="top">

Use Oracle Table Consumer, which is a Flowagent operator that uses Flowagent subengine for execution.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="b225dcb928944986901cbb24dff0e8ae.xml" text="" desc="" xtrc="xref:142" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

com.sap.dsp.templates.automl\_inference

</td>
<td valign="top">

Check later for information on this graph.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="5b127680538946a59f212838eeb9e735.xml" text="" desc="" xtrc="xref:144" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

graph com.sap.dsp.templates.automl\_training

</td>
<td valign="top">

Check later for information on this graph.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[Basic Training \(TensorFlow Training Template\)](basic-training-tensorflow-training-template-0acb903.md)

</td>
<td valign="top">

com.sap.dsp.templates.tensorflow\_training\_template

</td>
<td valign="top">

Provide a basic structure to use the Training operator to train TensorFlow models.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[HANA ML Inference on Dataset](hana-ml-inference-on-dataset-d854956.md)

</td>
<td valign="top">

com.sap.dsp.templates.hana\_ml\_inference\_on\_dataset\_template

</td>
<td valign="top">

Provide an example of a pipeline to expose a previously trained model and make inference on a provided dataset.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[HANA ML Inference on API Requests](hana-ml-inference-on-api-requests-def1b2c.md)

</td>
<td valign="top">

com.sap.dsp.templates.hana\_ml\_inference\_template

</td>
<td valign="top">

Expose a previously trained model as a REST endpoint.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[HANA ML Training Template](hana-ml-training-template-e83c21a.md)

</td>
<td valign="top">

com.sap.dsp.templates.hana\_ml\_training\_template

</td>
<td valign="top">

Create a model using HANA PAL functionality and store the artifact in SAP DI Data Lake.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[HANA ML Forecast Template](hana-ml-forecast-template-c9a9bdb.md)

</td>
<td valign="top">

com.sap.dsp.templates.hana\_ml\_forecast\_template

</td>
<td valign="top">

Provide an example of a pipeline to forecast data on-the-fly without the need of persisting a model.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[ML Batch Inference](ml-batch-inference-969d99d.md)

</td>
<td valign="top">

com.sap.dsp.templates.ml\_batch\_model\_serving\_template

</td>
<td valign="top">

Use file operators and Model Serving operator to deploy an ML model and run batch inference for a given set of images.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[ML Multi-Model Inference](ml-multi-model-inference-939fabf.md)

</td>
<td valign="top">

com.sap.dsp.templates.ml\_multi\_model\_serving\_template

</td>
<td valign="top">

Provide an example of an inference pipeline using the Model Serving operator to deploy multiple ML models and serve inference requests via HTTP/REST endpoint.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="2a351907e4764e3b8224d3cd0cbaddf3.xml" text="" desc="" xtrc="xref:160" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

com.sap.dsp.templates.python\_consumer\_template

</td>
<td valign="top">

Consume a trained ML model and expose it via API endpoint. The Python36 - Inference operator loads a model binary from Artifact Producer and receives input data from the OpenAPI Servlow operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="32fd2654d8554f0798a0046da53a3d59.xml" text="" desc="" xtrc="xref:162" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

com.sap.dsp.templates.python\_data\_preprocessing\_example

</td>
<td valign="top">

Undertake data preprocessing with Python, register a dataset, and submit metrics in an ML scenario.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

 <?sap-ot O2O class="- topic/xref " href="2e72cb0e27b24068a830938d42804c94.xml" text="" desc="" xtrc="xref:164" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiof327947dff9946c69bf18ca3e8c95bfc_en-US/src/content/localization/en-us/a25fe767e51e4c5b8c2eb09d24a7bff4.xml" ?> 

</td>
<td valign="top">

com.sap.dsp.templates.python\_producer\_template

</td>
<td valign="top">

Process data or train models using Python language in four steps.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[Pytorch Text Classification](pytorch-text-classification-207104a.md)

</td>
<td valign="top">

com.sap.dsp.templates.pytorch\_training\_example

</td>
<td valign="top">

Illustrate how to use the Training operator to train a supervised learning algorithm for classification using Pytorch, and submit metrics in an ML scenario.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[R Consumer - Consuming an ML Model via API using R Template](r-consumer-consuming-an-ml-model-via-api-using-r-template-de83c43.md)

</td>
<td valign="top">

com.sap.dsp.templates.r\_consumer\_template

</td>
<td valign="top">

Consume a trained ML model and expose it via API endpoint. The RClient - Inference operator loads a model binary from Artifact Producer and receives input data from the OpenAPI Servlow operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[R Consumer - Exposing a trained ML model via API Example](r-consumer-exposing-a-trained-ml-model-via-api-example-6e0e7e8.md)

</td>
<td valign="top">

com.sap.dsp.templates.r\_consumer\_example

</td>
<td valign="top">

Do inferences with a trained model from your ML sceneario.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[R Producer - Training an ML Model Using R Template](r-producer-training-an-ml-model-using-r-template-83e5c09.md)

</td>
<td valign="top">

com.sap.dsp.templates.r\_producer\_template

</td>
<td valign="top">

Train an ML model using R language in four steps.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[R Producer - Training a classification model using R Example](r-producer-training-a-classification-model-using-r-example-45a787e.md)

</td>
<td valign="top">

com.sap.dsp.templates.r\_producer\_classification\_example

</td>
<td valign="top">

Consume data from a CSV file stored in the Local File System \(vrep\) to train a classification model.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[R Producer - Training a regression model using R](r-producer-training-a-regression-model-using-r-f4f0fcf.md)

</td>
<td valign="top">

com.sap.dsp.templates.r\_producer\_regression\_example

</td>
<td valign="top">

Consume data from a CSV file stored in the Local File System \(vrep\) to create a linear regression model.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[TensorFlow MNIST Training Example](tensorflow-mnist-training-example-e9a04a7.md)

</td>
<td valign="top">

com.sap.dsp.templates.tensorflow\_mnist\_training\_example

</td>
<td valign="top">

Illustrate how to use the Training operator to train an image-classification model using the MNIST dataset with TensorFlow, and submit metrics in an ML scenario.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[Tensorflow Serving Template](tensorflow-serving-template-1dc735a.md)

</td>
<td valign="top">

com.sap.dsp.templates.tensorflow\_serving\_template

</td>
<td valign="top">

Provide an example of a basic online inference pipeline using the Model Serving operator to deploy an ML model and serve inference requests via HTTP/REST endpoint.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md)

</td>
<td valign="top">

[TensorFlow 2 and Scikit](tensorflow-2-and-scikit-4a0bd34.md)

</td>
<td valign="top">

com.sap.dsp.templates.tensorflow\_2\_training\_example

</td>
<td valign="top">

Illustrates how to use the Training operator to train a structured data classification model using a small dataset provided by the Cleveland Clinic Foundation for Heart Disease with TensorFlow 2, and submit metrics in an ML scenario.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Others](others-f410ca4.md)

</td>
<td valign="top">

[Jupyter Operator](jupyter-operator-417d0ab.md)

</td>
<td valign="top">

com.sap.dsp.templates.jupyter\_operator\_example

</td>
<td valign="top">

Open and run a notebook from a scenario in a pipeline, and it is meant to be modified as needed.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Integration](sap-integration-9a99c05.md)

</td>
<td valign="top">

[SAP Analytics Cloud Push Demo](sap-analytics-cloud-push-demo-6e727c1.md) 

</td>
<td valign="top">

com.sap.demo.sac.push

</td>
<td valign="top">

Push data to a dataset in SAP Analytics Cloud.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Integration](sap-integration-9a99c05.md)

</td>
<td valign="top">

[SAP CP EM Consumption Example](sap-cp-em-consumption-example-789a630.md)

</td>
<td valign="top">

com.sap.demo.cpem.consumption

</td>
<td valign="top">

Demonstrate the consumption of messages from SAP BTP Enterprise Messaging.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Integration](sap-integration-9a99c05.md)

</td>
<td valign="top">

[SAP CP EM Production Example](sap-cp-em-production-example-ec9764d.md)

</td>
<td valign="top">

com.sap.demo.cpem.production

</td>
<td valign="top">

Demonstrate the publication of messages via SAP BTP Enterprise Messaging.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[SAP Integration](sap-integration-9a99c05.md)

</td>
<td valign="top">

[SAP CPI-PI iFlow Example](sap-cpi-pi-iflow-example-d9c6de7.md)

</td>
<td valign="top">

com.sap.demo.cloud.cpi.pi

</td>
<td valign="top">

Demonstrate how the SAP CPI-PI iFlow operator interacts with connected operators.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[BW HANA View to File \(Full Load\)](bw-hana-view-to-file-full-load-b475df8.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.BW.bwDataTransferHANAView

</td>
<td valign="top">

Fetch data from a BW DataStore object and write it into a file \(S3\) target via HANA View.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Data Extraction from SAP S/4HANA CDS View to a File Store](data-extraction-from-sap-s-4hana-cds-view-to-a-file-store-e974798.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.ABAP.CDStoFile

</td>
<td valign="top">

Extract data from an ABAP CDS View to a file store and create related files in the file store

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Data Extraction from SAP S4/HANA CDS View to KAFKA](data-extraction-from-sap-s4-hana-cds-view-to-kafka-cd22a2c.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.ABAP.CDStoKafka

</td>
<td valign="top">

Extract data fom an ABAP CDS View to the KAFKA and create related messages.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Data Extraction using SLT to a File Store](data-extraction-using-slt-to-a-file-store-3fe72f0.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.ABAP.SLTtoFile

</td>
<td valign="top">

Extract data fom an ABAP table using SLT to a file store and create related files in the file store.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Data Extraction using SLT to KAFKA](data-extraction-using-slt-to-kafka-aef3e6b.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.ABAP.SLTtoKafka

</td>
<td valign="top">

Extract data from an ABAP table using SLT to the KAFKA and create related messages.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Ingest Files into HANA](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/7904dcd00ad9469fa92828fd3ec83089.html "Continuously ingests product data from CSV files into a HANA table. It lists all product*.csv files, reads their contents and loads into a HANA table.") :arrow_upper_right:

</td>
<td valign="top">

com.sap.scenarioTemplates.datalakeToDatabase.ingestToHana

</td>
<td valign="top">

Ingest product data from CSV files into a HANA table.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Initial Load + Delta Extraction from AnyDB](initial-load-delta-extraction-from-anydb-099adc5.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.ETLFromDB.cdcGraphGenerator

</td>
<td valign="top">

Use the Table Replicator operator for replication of relational databases.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Initial Load from any Table \(parallel\)](initial-load-from-any-table-parallel-727f84c.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.ETLFromDB.cdcInitialLoad

</td>
<td valign="top">

Read contents from an Oracle table and load it into a file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Data Services Transform Writing Data into Kafka](data-services-transform-writing-data-into-kafka-b804aaf.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.hybrid.remotedatatransform

</td>
<td valign="top">

Use the Data Services Transform operator to read data from a source and, through the Table to Message Converter operator, load it to the Kafka Producer operator on a specific topic. Then the data can be read back using the Kafka Consumer operator and shown in the Terminal operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Ingest Files Into SAP HANA \(Incremental Load\)](ingest-files-into-sap-hana-incremental-load-d0c7e3e.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.datalakeToDatabase.loadToHana

</td>
<td valign="top">

Load product data from CSV files into a HANA table.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Javascript File Data Manipulation](javascript-file-data-manipulation-2fc0a66.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.F2FJavascript

</td>
<td valign="top">

Manipulate data using a Javascript custom operator and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Ingest Files Into SAP HANA \(Incremental Load\)](ingest-files-into-sap-hana-incremental-load-d0c7e3e.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.datalakeToDatabase.loadToHana

</td>
<td valign="top">

Load product data from CSV files into a HANA table.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Node.js File Data Manipulation](node-js-file-data-manipulation-de3817c.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.F2FNode

</td>
<td valign="top">

Manipulate file data using Node.js and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Python File Data Manipulation with Pandas](python-file-data-manipulation-with-pandas-bbc1b87.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.F2FPython

</td>
<td valign="top">

Manipulate file data using Python with the Pandas library and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[R File Data Manipulation](r-file-data-manipulation-00e87fe.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.F2FR

</td>
<td valign="top">

Manipulate file data with an R custom operator and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Simple Javascript File Data Manipulation](simple-javascript-file-data-manipulation-29d8196.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2FJavascript

</td>
<td valign="top">

Manipulate file data using plain Javascript and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Simple Javascript File-to-DB Data Manipulation](simple-javascript-file-to-db-data-manipulation-88d58fd.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2DBJavascript

</td>
<td valign="top">

Manipulate file data using plain Javascript and writing the manipulated data to an SAP HANA database table.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Simple Javascript DB-to-File Data Manipulation](simple-javascript-db-to-file-data-manipulation-66f979b.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleDB2FJavascript

</td>
<td valign="top">

Manipulate data from an SAP HANA database table using plain Javascript and writing the manipulated data to a file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Simple Node.js File Data Manipulation](simple-node-js-file-data-manipulation-199c677.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2FNode

</td>
<td valign="top">

Manipulate data using Node.js \(without any libraries\) and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Simple Python File Data Manipulation](simple-python-file-data-manipulation-801a704.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2FPython

</td>
<td valign="top">

Manipulate data using plain Python with only built-in modules and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Simple R File Data Manipulation](simple-r-file-data-manipulation-bd5277e.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2FR

</td>
<td valign="top">

Manipulate data using plain R \(using only built-in libraries\) and writing the manipulated data back to another file.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Scenario Templates](scenario-templates-2739328.md)

</td>
<td valign="top">

[Simple R File-to-DB Data Manipulation](simple-r-file-to-db-data-manipulation-37af8cb.md)

</td>
<td valign="top">

com.sap.scenarioTemplates.customDataProcessing.simpleF2DBR

</td>
<td valign="top">

Manipulate data using plain R \(using only built-in libraries\) and writing the manipulated data to an SAP HANA database table.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Streaming Analytics](streaming-analytics-6ab9957.md)

</td>
<td valign="top">

[Connecting to Kafka in Streaming Analytics Project CCL](connecting-to-kafka-in-streaming-analytics-project-ccl-771105b.md)

</td>
<td valign="top">

com.sap.streaming.kafka

</td>
<td valign="top">

Use adapters to consume data from a Kafka topic that is produced using a Kafka Producer operator.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Streaming Analytics](streaming-analytics-6ab9957.md)

</td>
<td valign="top">

[Sending Datatypes to Streaming Analytics Projects](sending-datatypes-to-streaming-analytics-projects-b0166c9.md)

</td>
<td valign="top">

com.sap.streaming.types

</td>
<td valign="top">

Send data rows containing various streaming analytics column datatypes to a streaming analytics project.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Streaming Analytics](streaming-analytics-6ab9957.md)

</td>
<td valign="top">

[Streaming Analytics Freezer Monitor Demo](streaming-analytics-freezer-monitor-demo-bf3d248.md)

</td>
<td valign="top">

com.sap.streaming.demo

</td>
<td valign="top">

See a more complex graph involving streaming analytics operators.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Streaming Analytics](streaming-analytics-6ab9957.md)

</td>
<td valign="top">

[Using Adapters in Streaming Analytics Project CCL](using-adapters-in-streaming-analytics-project-ccl-1259ca9.md)

</td>
<td valign="top">

com.sap.streaming.adapters

</td>
<td valign="top">

This example graph shows how you can send and receive data to and from a streaming analytics project using adapters.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Utilities

</td>
<td valign="top">

[Wiretap](wiretap-1cbd846.md)

</td>
<td valign="top">

com.sap.demo.util.wiretap

</td>
<td valign="top">

Inspect messages that are transferred from one operator to another.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Utilities

</td>
<td valign="top">

[Wiretap 2](wiretap-2-378f0c8.md)

</td>
<td valign="top">

com.sap.demo.util.wiretap2

</td>
<td valign="top">

Inspect messages that are transferred from one operator to another.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Utilities

</td>
<td valign="top">

[Wiretap 3](wiretap-3-604dc68.md)

</td>
<td valign="top">

com.sap.demo.util.wiretap3

</td>
<td valign="top">

Inspect messages that are transferred from one operator to another.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Replication Flow: Merge Files](replication-flow-merge-files-360f527.md)

</td>
<td valign="top">

[Replication Flow: Merge CSV Files From Delta Load](replication-flow-merge-csv-files-from-delta-load-985e431.md)

</td>
<td valign="top">

com.sap.replicationFlow.csv.delta

</td>
<td valign="top">

Showcase how to merge small sized files that are generated by the Replication Management Service \(RMS\) tool into bigger, configurable sizes.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Replication Flow: Merge Files](replication-flow-merge-files-360f527.md)

</td>
<td valign="top">

[Replication Flow: Merge CSV Files From Initial Load](replication-flow-merge-csv-files-from-initial-load-97023bc.md)

</td>
<td valign="top">

com.sap.replicationFlow.csv.initialLoad

</td>
<td valign="top">

Showcase how to merge small sized files that are generated by the Replication Management Service \(RMS\) tool into bigger, configurable sizes.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Replication Flow: Merge Files](replication-flow-merge-files-360f527.md)

</td>
<td valign="top">

[Replication Flow: Merge Parquet Files From Delta Load](replication-flow-merge-parquet-files-from-delta-load-e267912.md)

</td>
<td valign="top">

com.sap.replicationFlow.parquet.delta

</td>
<td valign="top">

Showcase how to merge small sized files that are generated by the Replication Management Service \(RMS\) tool into bigger, configurable sizes.

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

[Replication Flow: Merge Files](replication-flow-merge-files-360f527.md)

</td>
<td valign="top">

[Replication Flow: Merge Parquet Files From Initial Load](replication-flow-merge-parquet-files-from-initial-load-4e79f77.md)

</td>
<td valign="top">

com.sap.replicationFlow.parquet.initialLoad

</td>
<td valign="top">

Showcase how to merge small sized files that are generated by the Replication Management Service \(RMS\) tool into bigger, configurable sizes.

</td>
<td valign="top">

 

</td>
</tr>
</table>

-   **[Examples Using Generation 1 Operators](examples-using-generation-1-operators-47a67ad.md "")**  

-   **[Examples Using Generation 2 Operators](examples-using-generation-2-operators-98af316.md "")**  

-   **[Scenario Templates](scenario-templates-2739328.md "Here, you'll find information on how to set up and run each scenario template we've
		prepared. ")**  
Here, you'll find information on how to set up and run each scenario template we've prepared.
-   **[Connectivity](connectivity-4cfe81e.md "")**  

-   **[Utilities](utilities-9d629fa.md "")**  

-   **[SAP Integration](sap-integration-9a99c05.md "")**  

-   **[Replication Flow: Merge Files](replication-flow-merge-files-360f527.md "")**  

-   **[Streaming Analytics](streaming-analytics-6ab9957.md "")**  

-   **[Examples](examples-ff56220.md "")**  

-   **[ML Scenario Manager Templates and Examples](ml-scenario-manager-templates-and-examples-ddd565e.md "")**  

-   **[Ingestion via Flowagent](ingestion-via-flowagent-139b202.md "")**  

-   **[Graph Snippets](graph-snippets-46542f8.md "")**  

-   **[Others](others-f410ca4.md "")**  


