<!-- loio8cda7c3a4ab74c86ba5752456418c4b0 -->

# Custom Editor

Use the Custom Editor to update the source dataset and projection and filters are pushed down to the source.

> ### Note:  
> The Custom Editor is only for the operators from the *Structured Data Operators* and *Connectivity \(via Flowagent\)* categories.



<a name="loio8cda7c3a4ab74c86ba5752456418c4b0__section_k2s_flf_h4b"/>

## Projection

Use the *Delete Projection* button to drop a column and reduce the amount of data read from the source.

> ### Note:  
> If you drop a column and need to revert the changes, use *Restore Metadata* to get the latest source dataset definition again.



<a name="loio8cda7c3a4ab74c86ba5752456418c4b0__section_n42_klf_h4b"/>

## Filters

Filtering is based on column capabilities. If a source allows filtering on a column, it is shown in the user interfaces as drop-down options.

Supported operators are EQUAL, BETWEEN, \>, <, <= and \>=.

If the operator user interface doesn’t show any filtering, then the source doesn’t support it. To filter on these columns, use the Data Transform operator.

> ### Note:  
> The operator OR is applicable per column while AND is applicable across columns. For example, a source has two columns: ID and NAME. If you choose multiple conditions on ID and on NAME, the query would look like \(ID = 2 OR ID = 3\) AND \(NAME = “TEST” OR NAME = “TEST2”\).



<a name="loio8cda7c3a4ab74c86ba5752456418c4b0__section_fyq_tlf_h4b"/>

## Data Preview

Use Data Preview to preview data in the source system.

Data Preview has two modes: Source and Adapted. Adapted Dataset takes the selected projection and applies a filter in the user interface, while Source Dataset shows the preview of the source object as-is.

**Related Information**  


[SAP Application Consumer V2](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/7a1527d494844adeb930d2e05cc1e56f.html "Use the SAP Application Consumer operator to consume data from SAP and non-SAP sources as modeled in a graph. Supported in Generation 2 graphs.") :arrow_upper_right:

[Structured File Consumer V3](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/02d49cc93994449f948094abf220ac3c.html "Structured File Consumer operator reads from any supported cloud storage. This operator is supported in Generation 2 graphs.") :arrow_upper_right:

