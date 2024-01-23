<!-- loio61d7208cd8c04d6f8d42a00bb9e59045 -->

# ABAP with Data Lakes

These graphs show how to ingest ABAP Tables or CDS Views data from SAP S/4HANA and SAP Business Suite systems into a cloud storage.



For both data source types, there are example graphs that showcase how to supply data lakes using a full or delta load mechanism.

A typical template scenario consists of a reader operator \(SLT Connector or CDS Reader\) that runs on a connected ABAP system. The connected ABAP system streams the data into a pipeline with a file writer or a Kafka producer operator.

> ### Note:  
> The ABAP system needs to fulfill the prerequisites documented in [2835207](https://me.sap.com/notes/2835207) before it can be connected to SAP Data Intelligence.



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

Data Extraction using SLT to a File Store [Data Extraction using SLT to a File Store](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/3fe72f0cde894aa6a19ea4d910be6aae.html "Extracts data fom an ABAP table using SLT to a file store and creates related files in the file store.") :arrow_upper_right: 

</td>
<td valign="top">

com.sap.scenarioTemplates.ABAP.SLTtoFile

</td>
<td valign="top">

Connect to an SAP Landscape Transformation Replication Server \(SLT\) configuration to read table data and write the data to a \(cloud\) storage or data lake.

</td>
</tr>
<tr>
<td valign="top">

Data Extraction using SLT to KAFKA [Data Extraction using SLT to KAFKA](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/aef3e6be31204adf8f8fd7d69adcc8a5.html "Extracts data fom an ABAP table using SLT to the KAFKA and creates related messages.") :arrow_upper_right: 

</td>
<td valign="top">

com.sap.scenarioTemplates.ABAP.SLTtoKafka

</td>
<td valign="top">

Connect to an SAP Landscape Transformation Replication Server \(SLT\) configuration to read table data and feed the data into a Kafka pipeline.

</td>
</tr>
<tr>
<td valign="top">

Data Extraction from SAP S/4HANA CDS View to a File Store [Data Extraction from SAP S/4HANA CDS View to a File Store](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/e9747985aa6546aeabe85b5bae50e8a4.html "In this example, the source is an SAP S/4HANA.") :arrow_upper_right: 

</td>
<td valign="top">

com.sap.scenarioTemplates.ABAP.CDStoFile

</td>
<td valign="top">

Connect to an SAP S/4HANA system to read CDS View Data and write the data to a cloud storage or data lake.

</td>
</tr>
<tr>
<td valign="top">

Data Extraction from SAP S4/HANA CDS View to KAFKA [Data Extraction from SAP S4/HANA CDS View to KAFKA](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/cd22a2cd6387487c9014fb19813dcd40.html "Extracts data fom an ABAP CDS View to the KAFKA and creates related messages.") :arrow_upper_right: 

</td>
<td valign="top">

com.sap.scenarioTemplates.ABAP.SLTtoKafka

</td>
<td valign="top">

Connect to an SAP S/4HANA system to read CDS View Data and feed the data into a Kafka pipeline.

</td>
</tr>
</table>

To learn how to set up and run each scenario template, see “Scenario Templates” in the *Repository Objects Reference for SAP Data Intelligence*. [Scenario Templates](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/2739328e6efc42be8cac62cf7dcfa449.html "Here, you'll find information on how to set up and run each scenario template we've prepared.") :arrow_upper_right: in the [Repository Objects Reference for SAP Data Intelligence](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/6529535176db4c489fa9baaa75af1b33.html "The Repository Objects Reference contains information about the built-in operators and graphs that SAP Data Intelligence provides for use in SAP Data Intelligence Modeler.") :arrow_upper_right:.

