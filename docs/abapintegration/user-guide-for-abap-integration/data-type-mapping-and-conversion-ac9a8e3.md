<!-- loioac9a8e3f0b7042b2ad0a4b73f6abda30 -->

# Data Type Mapping and Conversion

When extracting data from an ABAP-based source system and transferring it to a target system, it is not always possible to keep the data content and source format as-is \(for technical reasons\). Where necessary, the ABAP data types from the source are automatically replaced with their respective string representations during the data transfer. \(This is also known as wire format conversion.\)

For some of the **generation 1** ABAP operators, you can choose between the following options:

-   **Enhanced format conversion**: This conversion type not only changes the technical type \(which is necessary to allow a transfer at all\), but also validates the data. For example, values that the system considers "invalid" with respect to the applicable ISO standards are sent to the target as "NaN" \(Not a number\) or "undefined".

-   **Required conversions**: This conversion type changes some technical types without validation. For example, values that the system considers as invalid with respect to the applicable ISO standards are sent to the target without conversion, but as valid values. This version includes changes that are necessary to enable the transfer and cannot be skipped \(minimum scope\).

-   **Required conversions plus currency**: This conversion type changes some technical types without validation \(as described above for required conversions\) and converts currency values with regard to currency shift.

-   **Required conversions plus time format and currency**: This version of the wire format conversion changes some technical types without validation \(as described above for required conversions\), converts currency values respecting currency shift, and renders date or time formats in ISO format.


What options exactly you have depends on the available operator versions, and these in turn depend on the SAP S/4HANA version \(or DMIS version, respectively\) of your ABAP-based SAP system \(not on your version of SAP Data Intelligence Cloud.\) For more information, see the descriptions of the individual operators in the [Repository Object Reference](https://help.sap.com/docs/SAP_DATA_INTELLIGENCE/97fce0b6d93e490fadec7e7021e9016e/6529535176db4c489fa9baaa75af1b33.html?version=Cloud).

For the **generation 2** operator Read Data From SAP System and for **replication flows**, the conversion type **Required Conversions Plus Time Format and Currency** is used by default and cannot be changed.

For more information, including lists of the source data types that are changed during the transfer as well as the corresponding target formats, see SAP Note [3035658](https://me.sap.com/notes/3035658).

