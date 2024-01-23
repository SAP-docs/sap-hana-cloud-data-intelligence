<!-- loio866afc28b4374022ae5b109a936c42bd -->

# HANA to File

This scenario showcases how to read a table from a HANA database, modify it and write to a partitioned file on a remote file system in the CSV format.



In case of failures such as a network outage, the graph will fail and recover upon restart from the last snapshot saved, avoiding the need to read the whole table again. The generated file will be the same as long as the pipeline finishes, regardless of the graph had to recover or not.

The Python script is configured to read the HANA table and traverse it adding a new column to each row, showing both how to read, write, and traverse a table with the scripting API.

The table data is sent in batches by the HANA operator, with each message being streamed from one operator to another. The batch information available in the message headers is used by the [Write File](../data-intelligence-operators/write-file-7c3672c.md) operator to determine the index of each part file written to the target file system.

The Encode Table operator converts the tabular data received from the [Python3 Operator](../data-intelligence-operators/python3-operator-0211803.md) operator to a binary type for writing files, exposing options for file format, and specific details of each format, such as field delimiters.



<a name="loio866afc28b4374022ae5b109a936c42bd__section_qqv_31p_pqb"/>

## Operator Configuration

Aside from the standard configuration options of each operator, such as the connections to the database and file system, the following configurations are necessary for the scenario to run with the new features enabled:

-   [Read HANA Table V2](../data-intelligence-operators/read-hana-table-v2-b51aded.md)

    -   `Batching`: *Fixed size*


-   Encode Table
    -   `Collect Batches`: *False*


-   [Write File](../data-intelligence-operators/write-file-7c3672c.md)
    -   `File Mode`: *Partitioned file*





<a name="loio866afc28b4374022ae5b109a936c42bd__section_ttc_1bp_pqb"/>

## Run Configuration

Enable snapshot generation.

