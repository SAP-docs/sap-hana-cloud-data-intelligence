<!-- loiobf0b98fa83964bb395f8602a6569597b -->

# Ingest Google BigQuery SQL

This graph demonstrates how to use the SQL Consumer operator.



The SQL Consumer reads the data from a database and sends it to the next operator, which is then written into a file using the Structured File Producer. Only cloud storages are supported.



<a name="loiobf0b98fa83964bb395f8602a6569597b__section_ann_1jb_cgb"/>

## Components

-   Defining connection:

    sqlconsumer1: Provides connection to various databases.

    > ### Note:  
    > This operator should be configured before its usage.

-   Loader definition:

    structuredfileproducer1: Writes the content of the SQL Consumer result to a file.

    > ### Note:  
    > This operator should be configured before its usage.


