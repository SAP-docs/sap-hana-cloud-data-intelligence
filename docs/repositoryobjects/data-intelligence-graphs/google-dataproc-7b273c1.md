<!-- loio7b273c142e904c27861f627c02b3a50f -->

# Google Dataproc

This example shows how to submit a Spark job to an existing Google Dataproc cluster, and see the results of the job. In this example, we run the SparkPi example to calculate pi using Spark.



<a name="loio7b273c142e904c27861f627c02b3a50f__section_ntl_xlf_dfb"/>

## Prerequisites

-   A project on Google Cloud with access to the Dataproc service, the corresponding access key file as JSON, a running Dataproc cluster, and a Hadoop job.

The Spark examples jar can be found in the download of Spark found here: [https://spark.apache.org/downloads.html](https://spark.apache.org/downloads.html) 



<a name="loio7b273c142e904c27861f627c02b3a50f__section_rzy_lnb_t2b"/>

## Configure and Run the Graph

Follow the steps below to run the example from the SAP Data Intelligence Modeler UI:

1.  In the left panel, select the *Graphs* tab and open the Google Dataproc example graph.
2.  Open the configuration of the *Hadoop Job Submitter Operator*.
3.  Configure the connection by opening the connection dialogue box and choosing the correct connection from the Connection Manager app. Specify "spark" as the type of job.
4.  Below job type, enter the main jar file URI of the form "`gs://[your Google Storage Bucket]/[spark examples jar name].jar`". Below the URI, ensure the class name as "`org.apache.spark.examples.SparkPi`"
5.  In the tool bar, select *Run* \(play button\).
6.  The *Status* panel indicates if the graph is running.
7.  Use the context menu *Open UI* of the *Output* node to open the terminal. The bottom half shows the output and success messages of the Spark job.
8.  If the graph failed, you can find the logs for in the Google Storage bucket specified from the failing message.

