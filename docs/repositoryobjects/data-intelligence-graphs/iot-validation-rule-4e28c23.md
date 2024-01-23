<!-- loio4e28c239da0e43299757b4aa1aeac715 -->

# IoT Validation Rule

This graph models a sensor that tracks the temperature and surface illuminance of ice cream.



`Metadata Generator`generates sample metadata for a single sensor and passes it to `Metadata Producer`. `Metadata Producer` pushes the generated metadata to the Kafka cluster.

`Measurements Generator` generates sample sensor measurements and passes it to `Measurements Producer`. `Measurements Producer` pushes the generated sensor measurements to the Kafka cluster.

`Metadata Consumer` consumes the sample metadata, and`Measurements Consumer` consumes the generated sensor measurements.

`Stream Joiner` is a Javascript operator and joins sample sensor readings with its respective metadata. The joined output can be viewed with `Joined Output`.

`toCSVString`is a Javascript operator and converts the joined output to a CSV string.

`Validation Rule` tests the ice cream's temperature value is between -34.8°C and -24.8°C and the illuminance value is between 830 and 970 lux.

Sensor measurements that have passed the `Validation Rule` tests can be viewed with Pass Output.

Sensor measurements that have failed the `Validation Rule` tests can be viewed with Fail Output.

Detailed rule failure information can be viewed with `Fail Info Output`.

Any errors that may have occurred can be viewed with `Error Output`.



<a name="loio4e28c239da0e43299757b4aa1aeac715__section_rzb_3jc_v2b"/>

## Prerequisites

-   You need a running Kafka broker \(version 0.9.0 or greater\) and Zookeeper.




<a name="loio4e28c239da0e43299757b4aa1aeac715__section_qkg_hdc_v2b"/>

## Configure and Run the Graph

To run the example from the SAP Data Intelligence UI:

1.  Check the configuration of the `Metadata Generator`node: brokers and topic.
2.  Check the configuration of the `Measurements Generator` node: brokers and topic.
3.  Check the configuration of the `Metadata Consumer` node: brokers, topic \(must be the same as Metadata Consumer\), and kafkaVersion \(\>= 0.9.0\).
4.  Check the configuration of the Measurements Consumer node: brokers, topic \(must be the same as Measurements Generator\), and kafkaVersion \(\>= 0.9.0\)
5.  In the toolbar, select *Run* \(play button\). The *Status* panel indicates whether the graph is running.

> ### Note:  
> To view output of any terminal, activate the context menu of the desired terminal and select "Open UI".

