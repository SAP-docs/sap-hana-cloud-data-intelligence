<!-- loio4a784024937e425c822521ae38eea5a2 -->

# Working With Operators Based on the ABAP Language

The ABAP operators differ from other types of operators in that they do not come with SAP Data Intelligence Cloud. Rather, their implementations exist in their own repository \(called ABAP Pipeline Engine\) in the ABAP-based SAP system.



The modeler in SAP Data Intelligence Cloud contains a shell for each impementation of these ABAP operators so that you can work with them and include them in graphs \(pipelines\) in the same way as any other operator. To retrieve the relevant implementations from the ABAP-based SAP system, you need to provide an RFC connection.

The ABAP Pipeline Engine is included in the standard shipments for SAP S/4HANA Cloud and SAP S/4HANA \(as of SAP S/4HANA 1909\). For older releases \(NetWeaver 7.0 or higher\), you need to install the DMIS Add-on to get the ABAP Pipeline Engine.



<a name="loio4a784024937e425c822521ae38eea5a2__section_cjf_p5p_prb"/>

## Operator Generations and Versions

Two generations of operators are available. The generation 2 operators differ from the generation 1 operators in substantial ways. \(For example, the subscription feature has been replaced with a resilience feature.\) Consequently, it is not possible to combine generation 1 and generation 2 operators in one graph.

The existing versioning concept remains in place and is independent of operator generations.

For a description of all available operators and their respective features, see the Repository Objects Reference for SAP Data Intelligence Cloud:

-   Generation 1 \([ABAP](https://help.sap.com/viewer/97fce0b6d93e490fadec7e7021e9016e/Cloud/en-US/bde149c10dfc437f9e09d40c6be3fb2b.html)\)

-   Generation 2 \([ABAP](https://help.sap.com/viewer/97fce0b6d93e490fadec7e7021e9016e/Cloud/en-US/0f55b37f68f846e9959d936d7db0e0b1.html)\)


-   **[Creating a Custom ABAP Operator](creating-a-custom-abap-operator-761715f.md "This text describes the steps you need to perform in your ABAP-based SAP system to implement your own custom ABAP operator.")**  
This text describes the steps you need to perform in your ABAP-based SAP system to implement your own custom ABAP operator.

