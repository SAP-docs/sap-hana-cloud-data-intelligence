<!-- loiodaf699dda9294840aa7a448e68e3c75f -->

# Uploading Solution in System Management to Tenant or User Workspace



## Context

In this option you will upload your solution to the workspace of a given tenant or user in the SAP Data Intelligence cluster. The downside of this option is that it cannot be reversed easily. In the first option you can always remove a solution from a given strategy. On the other hand, in this option if some of the files in your solution overwrote some existing files in the tenant or user workspace, this will not be able to be reversed.



## Procedure

1.  First you need to compress your solution to a `.tar.gz` format: `tar -czf my_pysolution.tar.gz -C my_pysolution/ .`

2.  Log into your user in SAP Data Intelligence System Management and click the *File* tab at the top of the screen.

3.  Make sure no folder is selected in the *File* window.

    1.  For the *current user* - Click on *Import File* \> *Import Solution File* button on the *My Workspace* section.

    2.  For *all users* in your current tenant \(only possible for the tenant admin\) - Click on *Import File* \> *Import Solution File* button on the *Tenant Workspace* section


4.  In the popup window, select your `tar.gz` file and your solution will then be uploaded to the selected workspace.




<a name="loiodaf699dda9294840aa7a448e68e3c75f__result_erx_gwm_n2b"/>

## Results

You will be able to see the operators from your solution when you launch a new SAP Data Intelligence Modeler instance or restart the application.

