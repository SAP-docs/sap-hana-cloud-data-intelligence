<!-- loio22cb7912cc0a46ae870dae77664539f6 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Workspace Contains Files Larger Than 2 MB

If you have files larger than 2 MB in a workspace, you can adjust the file size limit through System Management.



## Context

You receive an error stating that the workspace for your scenario contains files that are larger than 2 MB.

You can retrieve a list of files that exceed the 2 MB limit by sending a GET request to <code>https://<i class="varname">&lt;cluster-domain-name&gt;</i>/app/ml-api/api/v1/scenarios/{scenarioId}/workspace</code>. The list of files is provided in the `details` attribute of the response.



## Procedure

Increase the file size limit as follows:

1.  Open the *System Management* application and click <span class="SAP-icons"></span> \(View Application Configuration and Secrets\).

2.  Click :pencil2: and search for the parameter that sets the file size limit \(*ML-API: Limit for the maximum size of a file in the workspace of an ML Scenario \(bytes\)*\).

3.  Increase the limit to the desired value.

4.  Click *Update*.

5.  Return to the *Applications* tab, find the entry for ML API, and restart it by clicking <span class="SAP-icons"></span> \(Play\).


