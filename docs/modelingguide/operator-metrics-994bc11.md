<!-- loio994bc115589d40929905dc401263ab10 -->

# Operator Metrics

The operators publish a set of metrics as soon as the graph is executed. Each operator provides a different set of metrics.

> ### Note:  
> Operator Metrics is currently relevant only for the operators from the Structured Data Operators and Connectivity \(via Flowagent\) categories.



<a name="loio994bc115589d40929905dc401263ab10__section_ymr_zbd_qnb"/>

## Consumer Operators

-   Optimized \(Boolean\): indicates whether the operator is optimized with other operators from the same engine. When this metric is set to 1, the runtime metrics, such as row count, aren’t displayed.
-   Row Count \(rows\): provides the number of rows read from the source.
-   Column Count \(columns\): provides the number of columns read from the source.
-   Partition Count \(partitions\): provides the number of partitions being read when the source is set to use partitions.



<a name="loio994bc115589d40929905dc401263ab10__section_l55_1cd_qnb"/>

## Producer Operators

-   Row Count \(rows\): provides the number of rows written to the target.
-   Current row rate \(rows/s\): provides the number of rows per second written to the target.
-   Batch count \(batches\): provides the number of batches written when the operator is set to write the data in batches.
-   Elapsed execution time \(seconds\): indicates the amount of time the graph has been running.



<a name="loio994bc115589d40929905dc401263ab10__section_pvx_hcd_qnb"/>

## Metrics Available in Debug Mode

-   Job CPU usage \(percentage\): indicates the CPU usage for the execution engine.
-   Job memory usage \(KB\): indicates the memory usage for the execution engine.
-   Operator CPU usage \(percentage\): indicates the CPU usage for the operator subengine.
-   Job memory usage \(KB\): indicates the memory usage for the operator subengine.

