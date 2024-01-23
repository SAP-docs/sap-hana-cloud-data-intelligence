<!-- loio55b2a17f987744cba62903e97dd99aae -->

# Loading and Replicating Data from ABAP CDS Views in SAP S/4HANA

To make the data from an ABAP CDS view available inSAP Data Intelligence Cloud, you need to specify specific annotations for the view in the ABAP Development Tool \(ADT Tool\).

> ### Note:  
> This applies to SAP S/4HANA, but **not** to SAP S/4HANA Cloud.

The annotations allow the view to use a trigger-based Change Data Capture \(CDC\) recording mechanism to load data and record changes to the tables that belong to the view.

The relevant annotations are described in the sections below.

> ### Note:  
> You can find detailed information about all the annotations mentioned in this document on the SAP Help Portal at [https://help.sap.com](https://help.sap.com). Search for `CDS Annotations` and select the entry for product SAP S/4HANA. Expand the node *CDS Annotations* and select the node *Analytics Annotations*.



**Loading Data from a CDS View**

To load data from a custom CDS view, add the following annotation to the view:

-   `Analytics.dataExtraction.enabled`


> ### Note:  
> Not all CDS views delivered by SAP have this annotation. You can view a list of the CDS views that already use this annotation by creating a query that uses a SELECT statement for the following CDS view:
> 
> -   `I_DataExtractionEnabledView`

Alternatively, you can use the data preview function in the SAP HANA Studio or ABAP Development tools for Eclipse.



**Replicating Data from a CDS View**

The Change Data Capture recording mechanism uses database triggers to record any changes to the tables that belong to an ABAP CDS view. To do this, the key fields of all underlying tables need to be mapped to the fields of the CDS view. For simple CDS views such as CDS projection views, this can be done automatically by using the following annotation:

-   `Analytics.dataExtraction.delta.changeDataCapture.automatic`


For more complex CDS views that use joins, the mapping must be done manually. You use the following annotation to do this:

-   `Analytics.dataExtraction.delta.changeDataCapture.mapping`




**Definition of Annotations**

The following code shows the options that are available for the annotations described above.

> ### Sample Code:  
> ```
> Annotation Analytics {
>   dataCategory : String(20) enum { DIMENSION; FACT; CUBE; AGGREGATIONLEVEL; };
>   dataExtraction: { 
>     enabled : Boolean default true;
>     delta : { 
>       changeDataCapture : {
>         automatic : Boolean default true;          
>         mapping : { 
>           role : String(30) enum {MAIN; LEFT_OUTER_JOIN_TO_ONE_JOIN;};
>           table : String(30);
>           viewElement : array of ElementRef;
>           tableElement : array of ElementRef;
>           filter : { 
>             tableElement : ElementRef;
>             operator : String(11) enum {EQ;NOT_EQ;GT;GE;LT;LE;BETWEEN;NOT_BETWEEN;} default #EQ;
>             value : String(45);
>             highValue : String(45);
>                     };
>               };
>             };
>           };
>          };
> ```

