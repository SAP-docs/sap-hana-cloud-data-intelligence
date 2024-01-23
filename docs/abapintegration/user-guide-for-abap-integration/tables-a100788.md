<!-- loioa100788cf10940c1a74aed86a5fa8f49 -->

# Tables

To extract data directly from tables, you additionally need SAP Landscape Transformation Replication Server \(SLT\), which acts as an intermediary between your data source and SAP Data Intelligence Cloud.



Proceed as follows:

1.  Set up a new SLT configuration in transaction `ltrc` of the SLT system. Choose the respective source system and use `SAP Data Intelligence` as the target. Note that you need to use different SLT configurations depending on whether you are working with operators of generation 1 or generation 2, respectively, or with replication flows. For more information, see the application help for [SLT](https://help.sap.com/slt).

2.  Once the SLT configuration is available, make a note of its 3-digit identifier \(mass transfer ID\).

3.  In the operator data \(or in the definition of the replication flow, respectively\), you can now enter the mass transfer ID as well as the name of the table you want to extract data from.


