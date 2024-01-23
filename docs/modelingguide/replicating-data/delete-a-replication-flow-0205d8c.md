<!-- loio0205d8cac1af4a8eae8130c423b64bdb -->

# Delete a Replication Flow

Delete SAP Data Intelligence replication flows or their associated tasks using the *Replications* editor in the Modeler interface.



<a name="loio0205d8cac1af4a8eae8130c423b64bdb__prereq_vqh_zbx_k5b"/>

## Prerequisites

Before you delete a replication flow from the shared repository, you must undeploy it. For more information, see [Undeploy a Replication Flow](undeploy-a-replication-flow-4e7d434.md).



## Context

You can delete a replication flow from your user repository or from the shared repository. In either case, existing versions of the replication flow remain in the other repository.

If you delete or undeploy a replication flow, the system does not delete the target table or the tasks even if the target table was created by the replication management system.

-   To delete a replication flow from your user repository, do the following:
    1.  On the *Replications* tab of the Modeler, in the left pane right-click the replication flow to delete.
    2.  Choose *Delete from user repository*.

-   To delete a replication flow from the shared repository, do the following:
    1.  On the *Replications* tab of the Modeler, display the replication flow to delete.
    2.  From the toolbar, choose the *Undeploy* icon.
    3.  Confirm the undeployment.


