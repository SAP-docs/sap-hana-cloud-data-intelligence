<!-- loio1c97a10cb49247d981ed30d53be38f73 -->

# Generation 1 and Generation 2 Operators

SAP Data Insight Modeler offers two generations of operators: Generation 1 \(Gen1\) and Generation 2 \(Gen2\).

Gen2 of vFlow operators communicate more efficiently between other Gen2 operators, but can't communicate with Gen1 operators. Therefore, when you create graphs in the Modeler, you first select either Gen1 or Gen2 operators.

Gen2 operators have the following advantages over Gen1 operators:

-   More efficient graph \(pipeline\) recovery from errors.
-   New structured types of native streaming of messages between operators.
-   Support for statemanagement \(snapshot\) and auto recovery of failed graphs.
-   Improved versions of Gen1 operators, such as the Python3 operator.

The following are the predefined Gen1 and Gen2 operator classifications:

-   Operators that connect to messaging systems, such as Kafka, MQTT, NATS, and WAMP.
-   Operators that store and read data, such as files, Hadoop Distributed File System \(HDFS\) and Amazon Simple Storage Service \(Amazon S3\).
-   Operators that connect databases, such as SAP HANA and SAP Vora.
-   Operators for the JavaScript engine that manipulate arbitrary data.
-   Process operators that run any program \(stateful and stateless\) for manipulating data in a graph.
-   Operators for data type conversion.
-   Operators for digital signal processing.
-   Operators for machine learning.
-   Operators for image processing.

> ### Remember:  
> Gen2 operators can't communicate with Gen1 operators. Therefore, you can create graphs with just one generation of operators or the other, but not combined.

