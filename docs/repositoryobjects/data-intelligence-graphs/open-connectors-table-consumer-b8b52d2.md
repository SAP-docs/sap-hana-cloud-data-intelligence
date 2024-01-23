<!-- loiob8b52d270d8f464cae90db80a2cc2c57 -->

# Open Connectors Table Consumer

This graph demonstrates how to use the SAP Application Consumer using the connection Open Connectors. It is a Flowagent operator and uses a Flowagent subengine for processing, so it needs to be connected to a Flowagent-based consumer operator to read the data.



Table Consumer reads the data from the source in batches \(N rows per call\) and loads the data to the next operator.



<a name="loiob8b52d270d8f464cae90db80a2cc2c57__section_irl_ptb_xhb"/>

## Components



### Defining Open Connectors connection

-   `sapapplicationconsumer1`: Provides consumer connection information. Choose an existing Open Connectors connection from Configuration Manager. Specify the source to load all data from that table.




### Flowagent Producer

-   `structuredfileproducer1`: Flowagent-based consumer requires a Flowagent-based producer like file, database, or CSV producer. Data is loaded by Flowagent and output to a target.




### Terminating Graph

-   `graphterminator1`: The processing graph ends after the Flowagent producer writes the data to the target.


