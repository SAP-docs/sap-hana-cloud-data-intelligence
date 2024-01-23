<!-- loio43e3eac6181147c49d2fc1cfd468eda5 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Send E-Mail Notifications

Use the Notification operator in the SAP Data Intelligence Modeler to send e-mail notifications to users at certain points during the data workflow execution.



<a name="loio43e3eac6181147c49d2fc1cfd468eda5__prereq_pwc_v2t_cfb"/>

## Prerequisites

Create a connection to an SMTP server using the SAP Data Intelligence Connection Management application.



## Context

A typical use case for using the notification operator is to send an e-mail when an operator writes onto its `error` or `success` port. The message body contains technical information that the notification operators receive at its input port from the previous operator in the data workflow.



## Procedure

1.  Start the SAP Data Intelligence Modeler.

2.  In the navigation pane, select the *Graphs* tab.

3.  In the navigation pane toolbar, choose :heavy_plus_sign:

    The application opens an empty graph editor in the same window, where you can define your graph.

4.  Select the operator.

    A graph can contain a single operator or a network of operators based on the business requirement.

    1.  In the navigation pane, choose the *Operators* tab.

    2.  In the search bar, search for the Notification operator.

    3.  In the search results, double-click the Notification operator \(or drag and drop it to the graph editor\) to add it as a process in the graph execution.


5.  Configure the operator.

    1.  In the graph editor, select the Notification operator and choose <span class="SAP-icons"></span> \(Open Configuration\).

    2.  In the *Connection* text field, enter the required connection ID.

        You can also browse and select the required connection.

    3.  If you want to delete the attachments after sending the e-mail, in the *Delete attachments after sending* dropdown list, select *true*.

    4.  In the *Default From Value* text field, enter the value of `email.from` that the Modeler must use when no such value is received through the incoming message.

    5.  In the *Default To Value* text field, enter the value of `email.to` that the Modeler must use when no such value is received through the incoming message.

    6.  In the *Default Subject Value* text field, enter the value of `email.subject` that the modeler must use when no such value is received through the incoming message.


    > ### Note:  
    > The following characters aren't supported in message header names: `<`, `>`, `$`, and `{}`.


