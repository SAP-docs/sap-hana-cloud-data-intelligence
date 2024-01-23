<!-- loio023c75aedfdd4646934f2d9ccde5660a -->

# Changing Data Capture \(CDC\)

SAP Data Intelligence supports CDC technology for some connection types.



<a name="loio023c75aedfdd4646934f2d9ccde5660a__section_xlc_nzs_kjb"/>

## Databases

The following databases support CDC capability by using a trigger-based approach for capturing changes:

-   DB2
-   HANA
-   MSSQL
-   MySQL
-   Oracle

Because creating the graph can become complex, SAP Data Intelligence provides a [Table Replicator V3 (Deprecated)](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/79fcadb91f584f868a6662111b92f6e7.html "Change Data Capture (CDC) is a delta capture technique that uses triggers for Insert, Update, and Delete to track the change history for a specific table. This operator is supported in Generation 1 graphs.") :arrow_upper_right: operator that helps you create the appropriate graphs.



<a name="loio023c75aedfdd4646934f2d9ccde5660a__section_wgm_4zs_kjb"/>

## Cloud Data Integration

Cloud Data Integration \(CDI\) supports polling-based CDC technology.

**Related Information**  


[Improving CDC Graph Generator Operator Performance](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/8709ef1f2c03489eb404496f20484411.html "The performance of the Change Data Capture (CDC) Graph Generator operator depends on the initial table size and how rapidly change data is generated in the source system.") :arrow_upper_right:

[CDC Graph Generator (Deprecated)](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/a69c62fbe76547e4b88617b2a0e7f700.html "Change Data Capture is a Delta Capture Technique using database-specific triggers for Insert, Update and Delete. Since manually creating the SQL per table is time consuming, this operator simplifies this.") :arrow_upper_right:

 <?sap-ot O2O class="- topic/link " href="93b5e5391e304c59996e4ba45cb7c422.xml" text="" desc="" xtrc="topicref:62" xtrf="file:/home/builder/src/dita-all/aaj1686154374413/loiofafe266fc7664785bb84cb7ab4822a2e_en-US/src/content/localization/en-us/cc6d420f2462481ebf668f705ee32f9e.ditamap" ?> 

