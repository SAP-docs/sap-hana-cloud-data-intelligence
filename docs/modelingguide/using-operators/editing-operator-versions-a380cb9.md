<!-- loioa380cb992149456c83265353b68085be -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Editing Operator Versions

You can edit an existing version of an operator.



## Procedure

1.  You can view the operator versions through the navigation pane or the graph editor:

    -   In the navigation pane, choose the *Operators* tab, right-click the operator, and choose *Show all versions* menu option.

    -   In the graph editor, right-click the operator and choose *Operator versions* menu option.

2.  In the *Operator versions* dialog, choose the :pencil2: \(Edit\) option.

    The operator version editor opens.

3.  To modify the existing configuration of the operator.

    1.  To provide the replacement operator if it’s a deprecated operator,

        1.  In the version editor of a deprecated operator, choose :pencil2: \(Enter Replacement Info\).
        2.  Enter the operator name with which you want to replace the deprecated operator.

    2.  To delete a version of the operator, in the *Operator Versions* dialog, select a version and click :wastebasket: \(Delete\).

        > ### Note:  
        > When you try to delete an operator version that is used in multiple graphs, you will encounter a warning message, as the deletion would result in failure of the graphs in which that version of the operator is used.

    3.  To view logs of a version of an operator, in the version editor, choose *View Change Log*.


4.  When the changes are complete, in the editor toolbar, choose :floppy_disk: \(Save\) to save the changes to the current version of the operator.


