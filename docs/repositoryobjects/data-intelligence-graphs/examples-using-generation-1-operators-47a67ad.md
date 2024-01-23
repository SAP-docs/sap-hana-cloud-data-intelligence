<!-- loio47a67adc49634dcf856778f2dc9dcfa8 -->

# Examples Using Generation 1 Operators

-   **[Data Generator](data-generator-cb7028b.md "The data generator generates arbitrary values simulating a set of sensors. The data is
		written to a terminal. You can see the generated data by opening the UI of the terminal
		operator.")**  
The data generator generates arbitrary values simulating a set of sensors. The data is written to a terminal. You can see the generated data by opening the UI of the terminal operator.
-   **[Go Data Generator](go-data-generator-20a10c8.md "The data generator generates arbitrary values simulating a set of sensors. The data is
		written to a terminal. You can see the generated data by opening the UI of the terminal
		operator.")**  
The data generator generates arbitrary values simulating a set of sensors. The data is written to a terminal. You can see the generated data by opening the UI of the terminal operator.
-   **[Message Generator](message-generator-8e326df.md "The message generator generates arbitrary values packed into a message, simulating a set
		of sensors. The data is written to a terminal. You can see the generated data by opening the
		UI of the terminal operator.")**  
The message generator generates arbitrary values packed into a message, simulating a set of sensors. The data is written to a terminal. You can see the generated data by opening the UI of the terminal operator.
-   **[Go Message Generator](go-message-generator-6ed1d0a.md "The message generator generates arbitrary values packed into a message, simulating a set
		of sensors. The data is written to a terminal. You can see the generated data by opening the
		UI of the terminal operator.")**  
The message generator generates arbitrary values packed into a message, simulating a set of sensors. The data is written to a terminal. You can see the generated data by opening the UI of the terminal operator.
-   **[File System](file-system-170742e.md "The Data Generator produces arbitrary data.")**  
The Data Generator produces arbitrary data.
-   **[Kafka](kafka-31675b8.md "The data generator generates arbitrary data and passes it to the Kafka producer. The
		Kafka consumer reads the data and writes it to a terminal. You can see the generated data by
		opening the UI of the terminal operator.")**  
The data generator generates arbitrary data and passes it to the Kafka producer. The Kafka consumer reads the data and writes it to a terminal. You can see the generated data by opening the UI of the terminal operator.
-   **[Histogram Simple Example](histogram-simple-example-805f652.md "In this simple graph, the first operator generates random numbers that are sent to the Histogram operator. The Histogram operator produces
		the histogram of its inputs as a Message with an integer array on its body and the range of the interval on its attributes. The message is
		then converted to string by the ToString Converter and sent to the HistogramPlotter, which finally plots it in the user interface.")**  
In this simple graph, the first operator generates random numbers that are sent to the Histogram operator. The Histogram operator produces the histogram of its inputs as a Message with an integer array on its body and the range of the interval on its attributes. The message is then converted to string by the ToString Converter and sent to the HistogramPlotter, which finally plots it in the user interface.
-   **[HTML Viewer](html-viewer-ec75129.md "This example graph simulates a Sales Campaign generating pseudorandom data for a large
		number of stores. The data is generated and structured at the Python3Operator and then
		passed as a String containing an HTML/CSS document that is displayed on HTML Viewer and
		constantly refreshed for the duration of the simulation.")**  
This example graph simulates a Sales Campaign generating pseudorandom data for a large number of stores. The data is generated and structured at the Python3Operator and then passed as a String containing an HTML/CSS document that is displayed on HTML Viewer and constantly refreshed for the duration of the simulation.
-   **[Load into SAP HANA](load-into-sap-hana-d57498a.md "The data generator produces sensor data as a CSV string. The data is loaded into SAP
		HANA and in parallel sent to a terminal, which you can use to see the generated
		data.")**  
The data generator produces sensor data as a CSV string. The data is loaded into SAP HANA and in parallel sent to a terminal, which you can use to see the generated data.
-   **[Go Operator and File Reader](go-operator-and-file-reader-775e229.md "This graph reads content from a file and uses the go operator to deal with the file
		content and name using different go functions and message type in the Go
		operator.")**  
This graph reads content from a file and uses the go operator to deal with the file content and name using different go functions and message type in the Go operator.
-   **[Simple Command Executor](simple-command-executor-3407cb7.md "In this simple graph the first 2 operators (Data Generator and ToBlobConverter) generate
		blobs, which are send to the input port stdin of the Command Executor. The
		Command Executor executes a build-in Unix command on the input and pipes the result to the
		output port stdout. The resulting blob can be visualized using the
		connected Wiretap operator. If an error occurs in the command executor it is send via the
		second output port stderr to terminate the graph.")**  
In this simple graph the first 2 operators \(Data Generator and ToBlobConverter\) generate blobs, which are send to the input port `stdin` of the Command Executor. The Command Executor executes a build-in Unix command on the input and pipes the result to the output port `stdout`. The resulting blob can be visualized using the connected Wiretap operator. If an error occurs in the command executor it is send via the second output port `stderr` to terminate the graph.
-   **[Simple Wiring](simple-wiring-682921b.md "Some operators are capable of connecting multiple connections from and to a single port as well as connecting between different port types
		that are supported by the automatic conversion of the pipeline engine. This graph directly connects three data generating operators of
		different output port types to a wiretap that is directly connected to a terminal and another wiretap.")**  
Some operators are capable of connecting multiple connections from and to a single port as well as connecting between different port types that are supported by the automatic conversion of the pipeline engine. This graph directly connects three data generating operators of different output port types to a wiretap that is directly connected to a terminal and another wiretap.
-   **[Binary to Table Example](binary-to-table-example-3c2f3b5.md "This graph takes generated CSV file input in binary format and converts the file
		contents to data type table format. The result is shown in a wiretap UI.")**  
This graph takes generated CSV file input in binary format and converts the file contents to data type table format. The result is shown in a wiretap UI.
-   **[Table to Binary Example](table-to-binary-example-59faafb.md "This graph takes generated input in data type table format and converts the data to CSV
		binary format. The result is shown in a wiretap UI.")**  
This graph takes generated input in data type table format and converts the data to CSV binary format. The result is shown in a wiretap UI.
-   **[Basic Validation Rule](basic-validation-rule-3e1b0c7.md "The Validation Rule operator evaluates input data against a rule. That is, a logical
		expression checking for particular values, null, not null, and so on. The user may define
		one or more rules and give each rule a meaningful name.")**  
The Validation Rule operator evaluates input data against a rule. That is, a logical expression checking for particular values, null, not null, and so on. The user may define one or more rules and give each rule a meaningful name.
-   **[IoT Validation Rule](iot-validation-rule-4e28c23.md "This graph models a sensor that tracks the temperature and surface illuminance of ice
		cream.")**  
This graph models a sensor that tracks the temperature and surface illuminance of ice cream.
-   **[Anonymization](anonymization-eee0a03.md "The anonymization operator helps protect the privacy of individuals by creating groups
		of similar records so you can discover statistically valid insights from your data without
		risking re-identification of individuals. The data is written to a terminal. While the graph
		is running, you can see the generated input data by opening the UI of the input terminal
		operator. Likewise, you can see the anonymized data by opening the UI of the output terminal
		operator while the graph is running.")**  
The anonymization operator helps protect the privacy of individuals by creating groups of similar records so you can discover statistically valid insights from your data without risking re-identification of individuals. The data is written to a terminal. While the graph is running, you can see the generated input data by opening the UI of the input terminal operator. Likewise, you can see the anonymized data by opening the UI of the output terminal operator while the graph is running.
-   **[Data Mask](data-mask-625e5df.md "The Data Mask operator protects the personally identifiable or sensitive information by
		covering all or a portion of the data. The data is written to a terminal. While the graph is
		running, you can see the generated input data by opening the UI of the input terminal
		operator. Likewise, you can see the masked data by opening the UI of the output terminal
		operator while the graph is running.")**  
The Data Mask operator protects the personally identifiable or sensitive information by covering all or a portion of the data. The data is written to a terminal. While the graph is running, you can see the generated input data by opening the UI of the input terminal operator. Likewise, you can see the masked data by opening the UI of the output terminal operator while the graph is running.
-   **[DQMm Address Cleanse](dqmm-address-cleanse-7eb9478.md "The DQMm Address Cleanse operator creates a request from data that can be passed to the
		DQMm Client operator to be sent to the service.")**  
The DQMm Address Cleanse operator creates a request from data that can be passed to the DQMm Client operator to be sent to the service.
-   **[DQMm Reverse Geo](dqmm-reverse-geo-5335ef1.md "Start this demo graph, which will automatically start invoking a series of
		operations.")**  
Start this demo graph, which will automatically start invoking a series of operations.
-   **[Person and Firm Cleanse](person-and-firm-cleanse-c519383.md "Parses and standardizes person and firm (business organization) data. The Person and Firm example graph shows how the Person and Firm
		Cleanse operator is configured with different types of input: firm, name in a single column, name in multiple columns, person or firm, and
		country or language or region input data.")**  
Parses and standardizes person and firm \(business organization\) data. The Person and Firm example graph shows how the Person and Firm Cleanse operator is configured with different types of input: firm, name in a single column, name in multiple columns, person or firm, and country or language or region input data.

