<!-- loio599586b1a9a84ca3a762289ed8d7a961 -->

# Clean Up Source Artifacts

Some situations, such as when an administrator deletes a tenant or connection, can result in unused source artifacts that you need to delete to avoid performance issues.

For SAP S/4HANA cloud, deactivation of the communication channel \(Communication Arrangement\) results in automated clean-up.

For Microsoft Azure SQL database:


<table>
<tr>
<th valign="top">

Situation

</th>
<th valign="top">

Result

</th>
<th valign="top">

Actions

</th>
</tr>
<tr>
<td valign="top">

A connection associated with a replication flow is deleted from Connection Management.

</td>
<td valign="top">

The replication flow no longer displays in the Modeler or Monitor.

</td>
<td valign="top">

Re-create the connection.

The audit log lists deleted connections with the event ConfigurationChange. See [Viewing Audit Logs](https://help.sap.com/viewer/300d97f4d57c4b329df8c83858ff67fb/Dev/en-US/456b1dcbec334329930ce4b24b5e589f.html "SAP Data Intelligence provides a comprehensive audit logging system, which includes events that are related to Data Protection Principles.") :arrow_upper_right:.

</td>
</tr>
<tr>
<td valign="top">

Either the tenant was deleted or a replication task was deleted. but the system cannot connect to the source system after three attempts.

</td>
<td valign="top">

Replication flow can no longer connect to the source.

</td>
<td valign="top">

Run the following statements for each subscribed table to delete replication artifacts where:

<code>${<i class="varname">&lt;SourceSchema&gt;</i>}</code> is the schema name of the source table.

<code>${<i class="varname">&lt;SourceTableName&gt;</i>}</code> is the source table name.

<code>${<i class="varname">&lt;RmsSchema&gt;</i>}</code> is the schema name of the replication artifacts, which is the same as the database user name that was specified when creating a source connection in Connection Management.

Drop triggers:

```
DROP TRIGGER ${<SourceSchema>}.${<SourceTableName>}_I_RMS_TRIG
DROP TRIGGER ${<SourceSchema>}.${<SourceTableName>}_D_RMS_TRIG
DROP TRIGGER ${<SourceSchema>}.${<SourceTableName>}_U_RMS_TRIG
```

Drop sequences:

```
DROP SEQUENCE ${<RmsSchema>}.RMS_${<SourceTableSchema>}_${<SourceTableName>}_SEQ1
DROP SEQUENCE ${<RmsSchema>}.RMS_${<SourceTableSchema>}_${<SourceTableName>}_SEQ2
```

Drop stored procedure:

```
DROP PROCEDURE ${<RmsSchema>}.RMS_${<SourceTableSchema>}_${<SourceTableName>}_PROC_V1
```

Drop shadow table for logging changed data:

```
DROP TABLE ${<RmsSchema>}.RMS_SHADOW_${<SourceTableSchema>}_${<SourceTableName>}
```



</td>
</tr>
</table>

