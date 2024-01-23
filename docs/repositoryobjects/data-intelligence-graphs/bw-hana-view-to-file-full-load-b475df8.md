<!-- loiob475df8726d5454bbe6f1fe7e79e45af -->

# BW HANA View to File \(Full Load\)

Fetches data from a BW DataStore object and writes it into a file \(S3\) target via HANA View.



In this example, the graph is configured to execute full load from 0EPM\_ADSO1 BW DataStore object to a file \(S3\) target.



<a name="loiob475df8726d5454bbe6f1fe7e79e45af__section_zmq_1vc_1kb"/>

## Prerequisites

-   A valid HANA\_DB connection.

-   A valid BW connection containing reference to the HANA\_DB connection via the ‘HANA DB Connection ID’ field of the BW connection.

-   A valid S3 connection to be used as target.

-   Check and load 0EPM\_ADSO1 BW Advanced DataStore object with data if it's empty and make sure that an external HANA view exists for it.

    > ### Note:  
    > Any unconnected output port will result in a graph failure.




<a name="loiob475df8726d5454bbe6f1fe7e79e45af__section_og5_sb2_1kb"/>

## Configure and Run

1.  Open the graph com.sap.scenarioTemplates.BW.bwDataTransferHANAView and click the Run button \(►\).

2.  Provide the following configuration substitutions: BW\_CONNECTION : BW Connection ID containing reference to a HANA\_DB connection. S3\_CONNECTION : S3 Connection ID as target. TARGET\_FOLDER : Target folder name. TARGET\_FILE : Target file name \(for example, TestFile.csv\).

3.  Click OK to run the graph to execute the full load.

4.  The "Status" panel indicates if the graph is running.

5.  Navigate to S3 to view the target files.


