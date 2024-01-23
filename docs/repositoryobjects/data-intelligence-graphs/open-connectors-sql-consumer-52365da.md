<!-- loio52365daf91094549b347d4eae3bfdd16 -->

# Open Connectors SQL Consumer

This graph demonstrates how to use Open Connectors SQL Consumer. Open Connectors SQL Consumer is a Flowagent operator and uses a Flowagent subengine for processing, so it needs to be connected to a Flowagent-based consumer operator to read the data.



Table Consumer takes in a standard SQL as input and it will read the table from the source piece-wise \(N rows per call\) and load to next operator in line.



<a name="loio52365daf91094549b347d4eae3bfdd16__section_hlt_frb_xhb"/>

## Components



### Defining Open Connectors Connection

-   `openconnectorssqlconsumer1`: Provides consumer connection information. Choose an existed Open Connectors connection from Configuration Manager or replace substitution variables listed in below Substitution variables section. Input a standard SQL into the native\_sql\_statement field to load and filter data. Supported SQL syntax is limited. See Open Connectors SQL Consumer operator document for details about supported syntax.




### Flowagent Producer

-   `flowagentcsvproducer1`: Flowagent-based consumer requires a Flowagent-based producer like file, database, or CSV producer. Data is loaded by Flowagent and outputs in a CSV format.




### Wiretap

-   `wiretap1`: Wiretap a connection between Flowagent CSV Producer and Graph Terminator.




### Terminating Graph

-   `graphterminator1`: When the Flowagent producer writes all data to the file, it will end the graph.




<a name="loio52365daf91094549b347d4eae3bfdd16__section_r42_vrb_xhb"/>

## Substitution variables

-   `OCN_INSTANCE_ID`: Open Connectors instance ID

-   `OCN_BASE_URL`: Open Connectors API base URL

-   `OCN_USER_SECRET`: Open Connectors user secret

-   `OCN_ORG_SECRET`: Open Connectors organization secret

-   `SQL_STATEMENT`: Standard SQL statement to query and filter data, like select Name from UserRole where Name like 'VP%'


