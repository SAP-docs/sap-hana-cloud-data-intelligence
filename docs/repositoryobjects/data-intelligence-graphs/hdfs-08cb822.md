<!-- loio08cb822029364e9c89bd3b30e19d9a60 -->

# HDFS

The Data Generator produces arbitrary data.



The data is written to files on HDFS by Write File. The files are stored in the directory `/tmp/demo/` \(of the specified bucket\). The file names follow the scheme `file_<counter>.txt`.

The Read File reads this file and the content is written to a terminal.



<a name="loio08cb822029364e9c89bd3b30e19d9a60__section_w4x_mhb_v2b"/>

## Configure and Run the Graph

Follow the steps below to run the example from the SAP Data Intelligence Modeler UI:

1.  In the left panel, select the *Graphs* tab and navigate to `com/sap/demo/hdfs`.
2.  Check the configuration of the *Write File* node: `hadoopNamenode, hadoopUser`
3.  Check the configuration of the *Read File* node: `hadoopNamenode, hadoopUser`
4.  In the tool bar, select *Run* \(play button\).
5.  The *Status* panel indicates if the graph is running.
6.  Use the context menu *Open UI* of the *Terminal* node to open the terminal.
7.  The terminal opens and you see the produced files and their content.



### Optional Step: Check the files on HDFS

1.  Connect to HDFS and browse the directory `/tmp/demo/` to see the produced files.

