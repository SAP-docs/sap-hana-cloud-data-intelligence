<!-- loio74598346f8be471f99285eb0ddd46424 -->

# Troubleshooting

Here you can find a list of known issues with ABAP integration in SAP Data Intelligence Cloud and their solutions.

-   You have started a pipeline with ABAP operators in SAP Data Intelligence Cloud and get an error message "Number of sessions exceeded” \(or similar\).

    **Solution**: This issue is related to the maximum number of sessions in ABAP Pipeline Engine. For more information, see SAP Note [2999448](https://me.sap.com/notes/2999448).

-   ABAP connection type check \(in the connection management for SAP Data Intelligence fails.

    **Solution**: see SAP Note [2849542](https://me.sap.com/notes/2849542).

-   You are trying to extract a CDS view in a generation 1 pipeline using the CDS Reader operator and receive an error message in the process logs like “CDS view <CDS View name\> does not support data extraction”.

    **Solution**: Make sure that you extract a CDS view that is enabled for extraction as well as delta extraction, for example by using the required annotations \(for a custom CDS view\) or choosing a standard CDS view that is enabled for extraction. See also [CDS Views](cds-views-15805a3.md).

-   A generation 1 pipeline that includes the SLT Connector operator fails with an error message like: “Subscription is already being used by another graph”.

    **Solution**: see SAP Note [3057246](https://me.sap.com/notes/3057246)

-   A generation 1 graph fails with an error message like “The graph failed with error "invalid character '\\xXX' in string literal""

    **Solution**: see SAP Note [3016338](https://me.sap.com/notes/3016338)

-   Table extraction using the generation 2 operator Read Data From SAP System fails, and you get an error message like: “Object does not exist in the source system”.

    **Solution**: see SAP Note [3143151](https://me.sap.com/notes/3143151) 


