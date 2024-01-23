<!-- loioe9c9996c5d42434f8ac6bf67de0728d5 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Configuring Operators

Each operator has parameters that you can configure based on the business requirements for the graph \(pipeline\).



<a name="loioe9c9996c5d42434f8ac6bf67de0728d5__prereq_qlg_dcl_pvb"/>

## Prerequisites

Ensure that the operator to configure is in a graph.



## Context



## Procedure

1.  Select the applicable operator in your graph.

2.  Select <span class="SAP-icons"></span> \(Open Configuration\).

    The *Configuration* pane opens at right. The parameters in the Configuration pane have default settings based on the operator. To customize the operator, enter new values to the parameters. Based on the operator type, you can specify values to the subengines configuration parameters.

    > ### Note:  
    > If multiple implementations exist for the operator, select the applicable subengine in which to run the operator. The default value is Main \(Pipeline Engine\). To select the applicable engine, choose :heavy_plus_sign:and choose a subengine from the list.

3.  To define new configuration parameters for the selected operator, perform the following substeps:

    1.  Select :heavy_plus_sign: in the *Configuration* pane.

        > ### Note:  
        > You can define configuration parameters only for some base operators. Therefore, :heavy_plus_sign: is available only for applicable operators.

    2.  Enter a name for the new configuration parameter in *Add Property*.

    3.  Choose the property type.

    4.  Enter a value in *Value*.

    5.  Select *OK*.



