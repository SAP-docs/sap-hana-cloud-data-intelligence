<!-- loio055bdbdac7824d53acb5fa5d3e7da019 -->

# CSV Producer

This graph demonstrates how to use the CSV Producer operator, mainly detailing the usability of the outMessage port.



An OData source is read and converted into CSV rows in batches of 100. The rows are sent to the Wiretap operator. Because the Wiretap preserves the message headers, the JavaScript Message operator inline detects when the last batch is written and signals the Graph Terminator to finish the graph processing.



<a name="loio055bdbdac7824d53acb5fa5d3e7da019__section_q34_zpb_xhb"/>

## Components



### Defining Consumer

-   `odataqueryconsumer1`: provides an OData consumer information, but any consumer can be used.




### Loader Definition

-   `flowagentcsvproducer1`: CSV producer which outputs source content in batches.

-   `wiretap1`: wiretap a connection between the Flowagent CSV Producer and Wait for Last batch.



### Wait for Last Batch

-   `jsmessageoperator2`: operator that will wait for the message.lastBatch attribute to be set to true, which outputs a message so that the graph can be terminated.




### Graph Termination

-   `graphterminator1`:ends the current graph processing.


