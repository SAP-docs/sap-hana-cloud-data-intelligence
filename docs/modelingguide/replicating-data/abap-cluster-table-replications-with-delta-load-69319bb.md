<!-- loio69319bbeeb684271aa0f026ed6c70894 -->

# ABAP Cluster Table Replications with Delta Load

Replications from ABAP cluster tables result in more complex operations on the target system if delta load is involved.

There's one large underlying database table \(the table cluster\) that holds the data of multiple "logical" tables \(the cluster tables\). The table cluster has a set of key columns that are common to all cluster tables. Every cluster table can have additional key columns. \(For more information about cluster tables, see [Cluster Name](https://help.sap.com/docs/ABAP_PLATFORM/c238d694b825421f940829321ffa326a/3482ebd9107c4ee0b70eb912465df566.html?version=1709.011#loio5e78f50d3566438195471f9d806f3078).\)

You must always select one of the "logical" cluster tables as the replication source.

When replicating cluster tables that include delta load, any change in the source table results in the following:

1.  Deletion of all records in the target that match the respective values of the key columns of the underlying table cluster.
2.  Insertion of all records from the source table that match the corresponding values of the keys of the underlying table cluster. This includes the newly inserted or modified records, and excludes the deleted records.

If the target is a cloud storage or a Kafka cluster, the above-mentioned delete using the key values of the underlying table cluster is indicated by a delete record, where the key columns that are only present in the cluster table but not in the underlying table cluster aren't specified. For cloud storage targets in CSV format, a "?" is used to indicate such an unspecified key value.

When replicating a cluster table that includes delta load to a Kafka cluster, the keys of the messages are determined using only the key columns of the underlying table cluster.

