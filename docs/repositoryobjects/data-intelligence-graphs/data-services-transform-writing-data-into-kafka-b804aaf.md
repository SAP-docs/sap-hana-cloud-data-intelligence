<!-- loiob804aaf0f3be4ecd8eddb9d73b3b3139 -->

# Data Services Transform Writing Data into Kafka

Use the Data Services Transform operator to read data from a source and, through the Table to Message Converter operator, load it to the Kafka Producer operator on a specific topic. Then the data can be read beack using the Kafka Consumer operator and shown in the Terminal operator.



## Prerequisites

To run this graph:

1.  Select the `Connection ID`, `Repository`, `Job Server`, and, optionally, `System Configuration` in the Data Services Transform operator.

2.  Inside the Data Services Transform operator, open the tab `Graphical Editor`, configure the field `Source` inside the **DataSource** operator and complete the modeling.

3.  In the `Configuration Substitutions` panel, configure the `KAFKA_BROKER` and the `KAFKA_TOPIC`.




<a name="loiob804aaf0f3be4ecd8eddb9d73b3b3139__section_xzn_ljq_rvb"/>

## Components

-   **Data Services Transform**

    dataservicestransform1: Move data from an SAP Data Services on-premise version to Data Intelligence cloud version using Kafka.

-   **Table To Message Converter** 

    tabletomessageconverter1: Receives a vType as input and then outputs the data as message content with a CSV body as a string.

-   **Kafka Producer**

    kafkaproducer1: Allows applications to send records or messages to topics on a Kafka cluster.

-   **Kafka Consumer**

    kafkaconsumer1: Consumes records or messages from a Kafka cluster.




<a name="loiob804aaf0f3be4ecd8eddb9d73b3b3139__section_ycb_1kq_rvb"/>

## Configuration Substitutions

-   `KAFKA_BROKER`: Specify the Kafka broker which handle the communication between the topics.

-   `KAFKA_TOPIC`: Specify the Kafka topic which records are stored and published.

