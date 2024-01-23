<!-- loio5bbb5776be7a4250996750e3a7230e96 -->

# SQL to File

This scenario showcases how to run a single or multiple Select statements and write the result set\(s\) to a partitioned file on a remote file system in the CSV format.



In case of failures such as a network outage, the graph will fail and recover upon restart from the last snapshot saved, avoiding the need to read the whole table again. The generated file will be the same as long as the pipeline finishes, regardless of the graph had to recover or not.

The queried data is sent in batches by the HANA operator, with each message being streamed from one operator to another. The batch information available in the message headers is used by the [Write File](../data-intelligence-operators/write-file-7c3672c.md) operator to determine the index of each part file written to the target file system.

The Encode Table operator converts the tabular data to a binary type for writing files, exposing options for file format and specific details of each format, such as field delimiters.



<a name="loio5bbb5776be7a4250996750e3a7230e96__section_g4l_kfp_pqb"/>

## Operator Configuration

Aside from the standard configuration options of each operator, such as the connections to the database and file system, the following configurations are necessary for the scenario to run with the new features enabled:

-   [Run HANA SQL V2](../data-intelligence-operators/run-hana-sql-v2-5796f97.md)

    -   `Transaction Level`: *Per statement*

    -   `Batching`: *Fized size*

-   Encode Table
    -   `Collect Batches`: *False*


-   [Write File](../data-intelligence-operators/write-file-7c3672c.md)
    -   `File Mode`: *Partitioned file*





<a name="loio5bbb5776be7a4250996750e3a7230e96__section_scq_xfp_pqb"/>

## Run Configuration

Enable snapshot generation.

