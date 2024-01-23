<!-- loio7eec494c03f747529cd637e2c2fd8d7c -->

# Loading Data from Data Lake to Database \(SAP HANA\)

These graphs show how to batch and stream process data.



<a name="loio7eec494c03f747529cd637e2c2fd8d7c__section_npg_dkp_zjb"/>

## Batch Processing

Batch processing graphs show how to load data in a batch from different cloud storages into an SAP HANA database. Batch in this context means that the Modeler loads all data available at runtime and stops the execution when all files are processed.



### Available Templates


<table>
<tr>
<th valign="top">

Template

</th>
<th valign="top">

Path

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Load Files into HANA [Ingest Files Into SAP HANA (Incremental Load)](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/d0c7e3e9b0dc4e5eb485c7f675cb1d82.html "With an incremental load, the SAP Data Intelligence Modeler application loads data continuously to an SAP HANA table from CSV or JSON files that are in cloud storage. The graph processes all existing files first, and then monitors the directory to load new or modified files.") :arrow_upper_right: 

</td>
<td valign="top">

com.sap.scenarioTemplates.datalakeToDatabase.loadToHana

</td>
<td valign="top">

Load product data from CSV files into an SAP HANA table, offering at-least-once guarantee between multiple graph runs.

</td>
</tr>
</table>



<a name="loio7eec494c03f747529cd637e2c2fd8d7c__section_b2w_mkp_zjb"/>

## Stream Processing

Stream processing graphs show how to load data in near real-time from different cloud storages into an SAP HANA database. Real-time in this context means that the graphs run continuously and read new files when available by polling repeatedly for changes on the connected file storage.



### Available Templates


<table>
<tr>
<th valign="top">

Template

</th>
<th valign="top">

Path

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Ingest Files into HANA [Ingest Files into HANA](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/7904dcd00ad9469fa92828fd3ec83089.html "Continuously ingests product data from CSV files into a HANA table. It lists all product*.csv files, reads their contents and loads into a HANA table.") :arrow_upper_right: 

</td>
<td valign="top">

com.sap.scenarioTemplates.datalakeToDatabase.ingestToHana

</td>
<td valign="top">

Ingest product data in parallel from CSV files into an SAP HANA table with a long-running graph, offering at-least-once guarantee between multiple graph runs.

</td>
</tr>
</table>

To learn how to set up and run each scenario template, see “Scenario Templates” in the *Repository Objects Reference for SAP Data Intelligence*. [Scenario Templates](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/2739328e6efc42be8cac62cf7dcfa449.html "Here, you'll find information on how to set up and run each scenario template we've prepared.") :arrow_upper_right: in the [Repository Objects Reference for SAP Data Intelligence](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/6529535176db4c489fa9baaa75af1b33.html "The Repository Objects Reference contains information about the built-in operators and graphs that SAP Data Intelligence provides for use in SAP Data Intelligence Modeler.") :arrow_upper_right:.

