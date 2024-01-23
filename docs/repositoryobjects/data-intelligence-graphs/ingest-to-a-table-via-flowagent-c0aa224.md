<!-- loioc0aa2245a86d43419482f47a471babe2 -->

# Ingest to a Table via Flowagent

This graph demonstrates how to use Table Producer to write to any supported service.



The Table Producer operator is a Flowagent-based producer operator, thus it needs to be connected to a Flowagent-based consumer operator.

This demo graph demonstrates how the Table Producer can be used together with other Flowagent-based producers.

In this example, we use the SAP Application Consumer and loading its content to a table that is defined in the Table Producer operator.

More details on how the consumers work can be seen in the consumer ingestion sample graphs.



<a name="loioc0aa2245a86d43419482f47a471babe2__section_ipm_vbc_xhb"/>

## Components



### Defining SAP Application Consumer

-   `sapapplicationconsumer1`: Reads data from a variety of SAP and non-SAP applications.

    > ### Note:  
    > This operator should be configured before its usage.




### Loader Definition

-   `tableproducer1`: Provides a loader to write data to database targets.

    > ### Note:  
    > This operator should be configured before its usage.

-   `wiretap1`: Wiretap a connection between two operators.

