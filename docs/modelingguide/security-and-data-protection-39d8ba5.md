<!-- loio39d8ba5fc426435b86fc100a83be68c5 -->

# Security and Data Protection

When you develop a threat model, you must consider how to protect your data and keep personal identifiable information \(PII\) private.



<a name="loio39d8ba5fc426435b86fc100a83be68c5__section_ytm_sgw_r5b"/>

## Data Protection and Privacy \(DPP\)

You, as a user of SAP Data Intelligence, are responsible for keeping the PII in your data private and secure. While SAP Data Intelligence acts as the data processor, you control the input and output of data processed through SAP Data Intelligence.

> ### Example:  
> The Modeler application runs graphs. However, you instruct the Modeler to process data in the graph in a specific way, and you initiate the graph to run.

SAP Data Intelligence doesn't audit log the input of personal or sensitive data from source systems, nor does it audit log transformations or ingestions into target systems. You, as the data owner \(the owner of the source and target systems\) are responsible to ensure traceability. You must instruct source and target systems to properly generate relevant audit logs so that you're compliant with local data protection and privacy laws.



<a name="loio39d8ba5fc426435b86fc100a83be68c5__section_h1y_qgw_r5b"/>

## Sensitive Information in Logs

The Modeler creates trace information logs and includes design time objects, such as solution files, custom operators, and pipeline descriptions. Therefore, ensure that you don't include sensitive information statically in those types of design time objects. Instead, use alternative methods for securing storage of connectivity information, such as the Connection Manager.



<a name="loio39d8ba5fc426435b86fc100a83be68c5__section_qrv_tgw_r5b"/>

## Audit Logging Recommendations

SAP Data Intelligence uses the Modeler to create and run data pipelines \(graphs\) that access source and target systems. Based on your DPP requirements, consider SAP Data Intelligence audit logging behavior. Then revise audit logging configuration in your source and target systems to comply with established DPP regulations, such as GDPR, to log security, configuration, personal data read, and change events for relevant data.

For more information about DPP, see “Data Protection and Privacy in SAP Data Intelligence” in the *Administration Guide*.

