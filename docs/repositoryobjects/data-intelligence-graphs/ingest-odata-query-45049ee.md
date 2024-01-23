<!-- loio45049ee1aafb4c178558f94cfedd98a8 -->

# Ingest OData Query

This graph demonstrates how to use OData Query Consumer to read data from a API which implements the protocol.



In this example, the OData Query Consumer is reading the resource `Orders` from the public test service `services.odata.org`. The result is then converted into CSV and written to a file. The ‘Query’ field of the OData Query Consumer supports many operations such as projections, filters, and so on.

Example:

-   Entity set: `Orders`

-   Projections: `Orders?$select=CustomerID,EmployeeID,Employee/LastName,Employee/FirstName&$expand=Employee`

-   Filters: `Orders?$filter=Employee/FirstName eq 'Steven'`




<a name="loio45049ee1aafb4c178558f94cfedd98a8__section_pk5_243_v2b"/>

## Components

-   Defining OData connection

    ODataqueryconsumer1: provides OData consumer connection information

-   Flowagent Producer

    flowagentcsvproducer1: Flowagent-based consumer requires a flowagent-based producer like file, database or CSV producer. The output of the OData is sent to the next operator.

-   wiretap1: wiretap a connection between two operators.
-   Terminating Graph

    graphterminator1: When the Flowagent producer writes the output to the file, it will end graph processing.


