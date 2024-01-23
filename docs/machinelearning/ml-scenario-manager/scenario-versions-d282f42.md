<!-- loiod282f427a86a45b2a46170e14d5c4283 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Scenario Versions

When you first create your ML scenario, ML Scenario Manager assigns version number 1. You can create additional versions of your scenario and, if required, return to a previous version and make modifications from there.

Version 1 of your scenario is always blank, meaning that it doesn't contain any artifacts such as notebooks or pipelines. As soon as you add an artifact, the system indicates that the version has changed by adding the <span style="color:#346187;"><span class="SAP-icons"></span></span> icon next to the version number. You can continue to work in this mode without having to create a new version. For example, you can execute or deploy pipelines directly from your draft version. Pipelines that are started from a draft version are indicated by the :warning: icon in the header. The same icon is used for executions that are started from a draft version.

If you have made changes to a scenario that you want to discard, you can revert the scenario to its previous state by clicking <span class="SAP-icons"></span> \(Revert to Last Version\).

To create a snapshot of your scenario for future reference, follow these steps:

1.  Click on the *Create Version* button in the scenario header.
2.  Enter a descriptive name or brief description for the scenario.
3.  Save the new version.

To access previous versions of a scenario:

1.  Go to the *Version History* page.
2.  Select the desired scenario from the overview. You'll see separate tiles representing each version. The most recent version will be at the top of the timeline. Each tile includes a description \(if available\) and the number and type of data artifacts within the scenario:


    <table>
    <tr>
    <td valign="top">
    
    <span class="SAP-icons"></span>
    
    </td>
    <td valign="top">
    
    number of datasets
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    <span class="SAP-icons"></span>
    
    </td>
    <td valign="top">
    
    number of notebooks
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    <span class="SAP-icons"></span>
    
    </td>
    <td valign="top">
    
    number of pipelines
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    :arrow_forward:
    
    </td>
    <td valign="top">
    
    number of executions
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    <span class="SAP-icons"></span>
    
    </td>
    <td valign="top">
    
    number of models
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    <span class="SAP-icons"></span>
    
    </td>
    <td valign="top">
    
    number of deployments
    
    </td>
    </tr>
    </table>
    

-   **[Creating a New Version of Your Scenario](creating-a-new-version-of-your-scenario-6298c4d.md "Whenever you make a change to your scenario, you may want to save the scenario as a new
		version. By doing so, you can return to a previous version of your scenario and make further
		modifications from there.")**  
Whenever you make a change to your scenario, you may want to save the scenario as a new version. By doing so, you can return to a previous version of your scenario and make further modifications from there.

