<!-- loio099adc5b14184bf0abaab0ea4bd31ed8 -->

# Initial Load + Delta Extraction from AnyDB

Demonstrates how to use CDC Graph Generator Operator for replication of relational databases.



The Table Replicator operator performs replication through trigger mechanism. At the first execution, the necessary triggers and procedures are created in the source system and an initial load is performed. For consecutive executions, only delta extraction is performed.

For more information, see the Table Replicator operator documentation.



<a name="loio099adc5b14184bf0abaab0ea4bd31ed8__section_smj_bvk_1kb"/>

## Prerequisite

Permission to create triggers, tables, and views in the source.

