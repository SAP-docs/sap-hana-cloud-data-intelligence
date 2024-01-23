<!-- loiod614ce5ab3fe47918d06c97dd0bd6673 -->

# Flowagent SQL Executor V1 \(Deprecated\)

The Flowagent SQL Executor performs an SQL Statement to any supported database. This operator is supported in Generation 1 graphs.



It uses Flowagent subengine to connect to the database. The specific SQL syntax depends on the specified database.

It provides a way to run SQL commands such as `CREATE`, `INSERT`, `DELETE`, and `UPDATE` in the database source. Multiple commands can be provided, where they must be separated by a specified separator \(default is `;`\). The output will be `success` if the commands were successfully run in the source. If a command fails, it throws an error, which the `outError` port catches, if it is mapped.

> ### Note:  
> This operator is not suitable for data ingestion use cases even though commands such as INSERT and UPDATE are supported. Sending multiple batches of input statements results in poor operator performance.



<a name="loiod614ce5ab3fe47918d06c97dd0bd6673__section_sq1_nf3_vdb"/>

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

Database type

</td>
<td valign="top">

service

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. Database on which the SQL statement\(s\) will be executed. Supported databases are displayed below.

Default: `""`

</td>
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

Optional. Object containing the connection parameters to an ODBC database.

-   **Data Source Name** \(Mandatory\): The data source name of your ODBC connection, which needs to be configured in *System Management* under `flowagent/odbc.ini` file.

    ID: `dsn`

    Type: `string`

    Default: `""`

-   **User** \(Mandatory\): ODBC connection user.

    ID: `user`

    Type: `string`

    Default: `""`

-   **Password** \(Mandatory\): ODBC connection password.

    ID: `password`

    Type: `string`

    Default: `""`




</td>
</tr>
<tr>
<td valign="top">

Oracle Connection

</td>
<td valign="top">

oracleConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Optional. Object containing the connection parameters to an Oracle database.

</td>
</tr>
<tr>
<td valign="top">

MSSQL Connection

</td>
<td valign="top">

microsoftsqlserverConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Optional. Object containing the connection parameters to a MSSQL database.

</td>
</tr>
<tr>
<td valign="top">

Azure SQL Database Connection

</td>
<td valign="top">

azuresqldbConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Optional. Object containing the connection parameters to an Azure SQL Database.

</td>
</tr>
<tr>
<td valign="top">

DB2 Connection

</td>
<td valign="top">

db2Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Optional. Object containing the connection parameters to a DB2 database.

</td>
</tr>
<tr>
<td valign="top">

HANA Connection

</td>
<td valign="top">

hanaConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Optional. Object containing the connection parameters to a HANA database.

</td>
</tr>
<tr>
<td valign="top">

SAP HANA Data Lake Database Connection

</td>
<td valign="top">

hdldbConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Optional. Object containing the connection parameters to a SAP HANA Data Lake database.

</td>
</tr>
<tr>
<td valign="top">

MySQL Connection

</td>
<td valign="top">

mysqlConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Optional. Object containing the connection parameters to a MySQL database.

</td>
</tr>
<tr>
<td valign="top">

Redshift Connection

</td>
<td valign="top">

redshiftConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. Object containing the connection parameters to a Redshift database.

</td>
</tr>
<tr>
<td valign="top">

SAP IQ Connection

</td>
<td valign="top">

sapiqConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. Object containing the connection parameters to a SAP IQ database.

</td>
</tr>
<tr>
<td valign="top">

Snowflake Connection

</td>
<td valign="top">

snowflakeConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. Object containing the connection parameters to a Snowflake database.

</td>
</tr>
<tr>
<td valign="top">

Teradata Connection

</td>
<td valign="top">

teradataConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory. Object containing the connection parameters to a Teradata database.

</td>
</tr>
<tr>
<td valign="top">

Google BigQuery Connection

</td>
<td valign="top">

gbqConnection

</td>
<td valign="top">

object

</td>
<td valign="top">

Mandatory: Object containing the connection parameters to a Google BigQuery database.

</td>
</tr>
<tr>
<td valign="top">

SQL Statement\(s\)

</td>
<td valign="top">

sqlStatements

</td>
<td valign="top">

string

</td>
<td valign="top">

Optional. SQL statement\(s\) that are standard to the source. Statements must be separated by a specified separator.

Default: `""`

</td>
</tr>
<tr>
<td valign="top">

Separator

</td>
<td valign="top">

separator

</td>
<td valign="top">

string

</td>
<td valign="top">

Optional. Separator that will be used to split the input into SQL statements.

Default: `";"`

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

Optional. Set session parameters that affect the connection with the source.

Default: `""`

</td>
</tr>
</table>



<a name="loiod614ce5ab3fe47918d06c97dd0bd6673__section_knq_5f3_vdb"/>

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

sql

</td>
<td valign="top">

string

</td>
<td valign="top">

SQL statements that are standard to the source. Statements must be separated by a defined separator.

</td>
</tr>
</table>



<a name="loiod614ce5ab3fe47918d06c97dd0bd6673__section_swc_cg3_vdb"/>

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

result

</td>
<td valign="top">

string

</td>
<td valign="top">

Output `success` if the commands were successfully executed.

</td>
</tr>
<tr>
<td valign="top">

outError

</td>
<td valign="top">

string

</td>
<td valign="top">

If mapped, the operator errors are sent to this port and the graph continues running. If not mapped, the graph terminates with the operator error.

</td>
</tr>
</table>

