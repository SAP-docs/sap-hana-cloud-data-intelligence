<!-- loio249c0989e8e348a3870d69af121e6aa9 -->

# ODBC SQL Consumer \(Deprecated\)

Performs an SQL query to any database that provides an Open Database Connectivity \(ODBC\) connector.



It uses the Flowagent subengine to connect to the database. To establish an ODBC connection, a Data Source Name \(DSN\) must be provided, specifying the DSN properties. The DSN must be defined in a file, following the UNIX standard. To effectively read from it, it is necessary to connect this operator to a Flowagent-based producer operator \(for example, Flowagent CSV Producer\).

For more information on Data Source Name \(DSN\), see section **Configure Data Source Name \(DSN\)**.



<a name="loio249c0989e8e348a3870d69af121e6aa9__section_sq1_nf3_vdb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

ID

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

ODBC Connection

</td>
<td valign="top">

odbcConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. The object containing the connection parameters to an ODBC database.

</td>
</tr>
<tr>
<td valign="top">

Data Source Name

</td>
<td valign="top">

dsn

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The data source name of your ODBC connection, which needs to be configured in System Management.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

User

</td>
<td valign="top">

user

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. ODBC connection user.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Password

</td>
<td valign="top">

password

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. ODBC connection password.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Native SQL

</td>
<td valign="top">

native\_sql\_statement

</td>
<td valign="top">

string

</td>
<td valign="top">

SQL statement that is used to read from the source. The syntax depends on the underlying source.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Partition Type

</td>
<td valign="top">

partitionType

</td>
<td valign="top">

string

</td>
<td valign="top">

Partitioning is used to enable data reading in parallel. In this case, the producer must be inside a group with multiplicity equal to the number of partitions \(**only** the producer, for example, Flowagent File Producer\).

Default: "None"

</td>
</tr>
<tr>
<td valign="top">

Logical Partition Specification

</td>
<td valign="top">

partitionSpecification

</td>
<td valign="top">

object

</td>
<td valign="top">

For more information, see [Partitioning](partitioning-86085d9.md).

</td>
</tr>
<tr>
<td valign="top">

Additional Session Parameters

</td>
<td valign="top">

additionalSessionParameters

</td>
<td valign="top">

string

</td>
<td valign="top">

Set session parameters that affect the connection with the source.

Default: ""

</td>
</tr>
<tr>
<td valign="top">

Fetch Size

</td>
<td valign="top">

fetchSize

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the number of rows that will be fetched from the source in each request. For wide tables, smaller values are better. For tables with fewer columns, larger values are better.

Default: 1000

</td>
</tr>
</table>



<a name="loio249c0989e8e348a3870d69af121e6aa9__section_knq_5f3_vdb"/>

## Input


<table>
<tr>
<th valign="top">

Input

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`inSQL` 

</td>
<td valign="top">

string

</td>
<td valign="top">

MySQL table name from which the data will be read, usually in `<Schema>.<TableName>` format.

> ### Note:  
> This is optional. It can be overridden by Native SQL, so this port can also be used as a trigger.



</td>
</tr>
</table>



<a name="loio249c0989e8e348a3870d69af121e6aa9__section_swc_cg3_vdb"/>

## Output


<table>
<tr>
<th valign="top">

Output

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`outConfig` 

</td>
<td valign="top">

string.flowagent.config

</td>
<td valign="top">

Flowagent type port, which only `Flowagent producers` can consume \(for example, Flowagent File Producer\). To get the data as string, `Flowagent CSV Producer`can be used as producer.

</td>
</tr>
<tr>
<td valign="top">

`outError` 

</td>
<td valign="top">

string

</td>
<td valign="top">

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>



<a name="loio249c0989e8e348a3870d69af121e6aa9__section_zz1_zgd_qnb"/>

## Configure Data Source Name \(DSN\)

ODBC uses DSN to connect to the sources, and each database has its own configuration parameters in the DSN definition.

To configure a DSN, you must:

1.  Start the System Management application from the Launchpad.
2.  Choose the *Files* tab.
3.  In the *User Workspace*, create a folder named `flowagent` under the folder `files`.
4.  Right-click the `flowagent` and create a file called `odbc.ini`.
5.  In the `odbc.ini`, you must add the DSN configuration in a UNIX style.

> ### Note:  
> In the DSN definition, `/vrep` is equivalent to the files folder in the top level of the System Management files.

