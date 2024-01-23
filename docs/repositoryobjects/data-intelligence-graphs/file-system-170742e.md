<!-- loio170742e2134e4d98bc7d2c0c758041fa -->

# File System

The Data Generator produces arbitrary data.



The data is written to files on File System by Write File. The files are stored in the directory `./tmp/demo/` \(where `./` is the current working directory, for example, where the Data Pipeline Engine was started\). The file names follow the scheme `file_<counter>.txt.`

The Read File reads this file and the content is written to a terminal.



<a name="loio170742e2134e4d98bc7d2c0c758041fa__section_ft5_prb_v2b"/>

## Configure and Run the Graph

Follow the steps below to run the example from the SAP Data Intelligence Modeler UI:

1.  In the left panel, select the *Graphs* tab and navigate to `com/sap/demo/file`.
2.  In the tool bar, select *Run* \(play button\).
3.  The *Status* panel indicates if the graph is running.
4.  Use the context menu *Open UI*of the *Terminal* node to open the terminal.
5.  The terminal opens and you see the produced files and their content.

