<!-- loio188dfd9354de40a7b9041936c82a34b0 -->

# Information for System Administration

Some aspects of system administration for SAP Data Intelligence Cloud are specific to ABAP integration.



<a name="loio188dfd9354de40a7b9041936c82a34b0__section_b13_hs5_hvb"/>

## General

-   For an overview of general parameters in the context of ABAP integration \(for example regarding retention periods\), see SAP Note [3044005](https://me.sap.com/notes/3044005).

-   If you want to use Secure Network Communication \(SNC\), consider the information provided under [Configure Secure Network Communication for ABAP](https://help.sap.com/docs/SAP_DATA_INTELLIGENCE/ca509b7635484070a655738be408da63/9d7ce0ff15ad4d75940f888f862de855.html?version=Cloud).

-   For more information about parallel sessions in the context of ABAP integration, or if you get an error message that the maximum number of sessions was exceeded, see SAP Note [2999448](https://me.sap.com/notes/2999448).




<a name="loio188dfd9354de40a7b9041936c82a34b0__section_rrh_ft5_hvb"/>

## ABAP Connection Provider \(Axino\)

Axino is a feature for establishing connections between remote ABAP-based SAP systems and SAP Data Intelligence Cloud and enabling bidirectional data transfer. As a rule, Axino runs in the background using default settings, and there is no user interaction required. If necessary, however, you can change some settings in the System Management app of SAP Data Intelligence Cloud as follows:

-   Using **core dump files** in connection with Axino issues: If Axino crashes and you are unable to reproduce the issue or find a root cause, you can enable generation of core dump files and send the resulting files to SAP for further analysis. For more information as well as a detailed how-to description, see SAP Note [3033853](https://me.sap.com/notes/3033853).

-   **Auto-scaling**: As a rule, Axino runs in the background in one service instance of SAP Data Intelligence Cloud and uses default settings, and there is no user interaction required. However if the number of workload requests becomes very high, the available CPU or memory capacity may no longer be sufficient, and as a consequence subsequent requests run into performance issues and ‘out of memory’ errors. If this happens, you can try switching on the scale-out feature to use multiple service instances and balance the workload.

    Alternatively \(if auto-scaling is disabled\), you can define upper limits for the memory resources and CPU resources of your Axino pod.

    For further information, see SAP Note [3148794](https://me.sap.com/notes/3148794).


