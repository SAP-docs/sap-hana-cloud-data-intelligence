<!-- loiob9b819c2df404295beafe8c45de6606b -->

# Kafka as Target

In a replication flow, every source dataset is transferred to a respective topic in the Kafka cluster.

The target dataset name is matched to the topic name in the Kafka cluster.

> ### Note:  
> You can edit the name of the target topic, so it does not need to be the same as the source dataset.

Schema registries are not supported. If you choose AVRO as the serialization format, the schema is contained in every message. For JSON serialization format, no schema information is provided.

Each record from the source system is transferred into a single message in the selected target topic. The software does not load each batch set of data into a message.

The key of the messages is the combination of all primary key values of the record concatenated by "\_".

Additional headers are set in the messages:

> ### Note:  
> For information about configuring Kafka target options like number of partitions and replication factor, see [Create a Replication Flow](create-a-replication-flow-a425e34.md).

-   kafkaSerializationType: AVRO or JSON

    > ### Note:  
    > If you select AVRO, the columnName must consist of only alphanumeric and underscore characters and it must also start with a letter or an underscore

-   opType: Identifies the type of target row:
    -   *L*: Written as part of the initial load.

    -   *I*: After the initial load completed, new source row added.

    -   *U*: After the initial load completed, after image of an update to a source row.

        > ### Note:  
        > For some sources the system switches the value *U* to *A* after you apply SAP Note [3044005](https://me.sap.com/notes/3044005). The APE\_KEEP\_UPDATE\_OPERATION parameter is described in the SAP Note.

    -   *B*: After the initial load completed, before image of an update to a source row. These records are only sent by some sources \(like SAP HANA\) and only when the after image of the update is not passing the filters specified in the replication task.

    -   *X*: After the initial load completed, source row deleted. The only target columns to contain data for this operation code are codes that reflect the source key columns. All other target columns are empty.

    -   *M*: After the initial load completed, archiving operations.


-   Seq: Sequence number, an integer value that reflects the sequential order of the delta row in relation to other deltas. This column is empty for initial load rows and is not populated for all source systems \(for example, ABAP\).

> ### Note:  
> If the Kafka cluster is behind an SAP Cloud Connector \(SCC\), the Kafka cluster and the SCC must be configured such that the broker addresses advertised by the cluster match the virtual hosts maintained for the brokers in the SCC. The simplest solution is to use the same value for virtual and internal hosts in the SCC and to maintain no dedicated advertised listeners for the Kafka brokers. If advertised listeners are maintained, these must be used as virtual hosts in SCC and as broker addresses in the DI connection definition.

**Related Information**  


[Create a Replication Flow](create-a-replication-flow-a425e34.md "The SAP Data Intelligence Modeler includes an interface for creating and running replication flows.")

