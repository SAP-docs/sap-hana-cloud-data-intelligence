<!-- loio734a58abd8514078a5a3abb0a7e5061d -->

# Ingest Google BigQuery Table Producer

A Table Consumer is used to read data from a connection that can be configured, which is then converted into CSV and written into GCS via the Structured File Producer operator.



The Google BigQuery operator then reads the file from GCS and uses it to create a table on BigQuery.



<a name="loio734a58abd8514078a5a3abb0a7e5061d__section_nbs_fmb_cgb"/>

## Components

-   Source Data:

    tableconsumer1: provides a connection to various databases, but any consumer can be used.

    > ### Note:  
    > This operator should be configured before its usage.

-   Load to GCS:

    structuredfileproducer1: writes data into GCS, which is a necessary pre-requisite to use the Google BigQuery Producer operator.

    > ### Note:  
    > This operator should be configured before its usage.

-   Defining Connection:

    googlebigquerytableproducer1: creates tables into Google BigQuery.




<a name="loio734a58abd8514078a5a3abb0a7e5061d__section_jsv_z3y_3qb"/>

## Substitution Variables

-   ORACLE\_CONNECTION: Oracle connection to be used.
-   ORACLE\_SOURCE\_TABLE: Oracle table where the data is read, in the format <Owner\>.<Table\>.
-   GCS\_CONNECTION: Google Cloud Storage connection to be used.
-   GCS\_FILE\_NAME: Path to the file where the converted Oracle table contents are written to.
-   GBQ\_TARGET\_TABLE: Table created on Google BigQuery, in the format <Owner\>.<Table\>.

