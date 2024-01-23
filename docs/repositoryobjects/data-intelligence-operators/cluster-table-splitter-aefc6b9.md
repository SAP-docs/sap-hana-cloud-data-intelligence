<!-- loioaefc6b9f14b84942989df550a81faa07 -->

# Cluster Table Splitter

Use the Cluster Table Splitter to replicate one or more \(but not all\) logical tables for a cluster table.



> ### Note:  
> This operator is only relevant for the following releases:
> 
> -   DMIS 2011 SP18 and higher
> 
> -   DMIS 2018 SP03 to SP06 \(without TCI\)
> 
> -   SAP S/4HANA 1909 - Basis SP01 plus TCI Note 2873666
> 
> -   SAP S/4HANA 2020 - initial version
> 
> 
> For all later releases and versions, this operator is no longer relevant, in particular for the following:
> 
> -   DMIS 2018 SP06 plus TCI Note 3110660 as well as SP07 and higher
> 
> -   SAP S/4HANA 1909 - any SP plus TCI Note3105890 as well as SP05 and higher
> 
> -   SAP S/4HANA 2020 - any SP plus TCI Note 3105880 as well as SP03 and higher
> 
> -   SAP S/4HANA 2021 - any version
> 
> 
> Please use the new operator called `Read Data From SAP System` that is available in the `Modeler` in SAP Data Intelligence.

A cluster table in the ABAP-based remote system can consist of more than one logical table. The SLT Connector operator can read only the complete cluster table and provides you with the data of all logical tables. If you are interested only in some of the logical tables, you can use the Cluster Table Splitter operator to split a cluster table into its individual logical tables and then replicate only the logical tables you actually need.

To do so, you create an output port for each of the relevant logical tables, using the name of the logical table as the name of the output port. An output port can be connected to a subsequent operator. For V0 and V1 of the Cluster Table Splitter operator \(that have output type abap.\*\), you can use the ABAP Converter operator to convert the data into string, XML, or JSON according to the settings of the output format.



## Example

You want to replicate the logical table named `BSEG`, which is a logical table in cluster table `RFBLG`. To do so, you enter `RFBLG` as the table name for SLT Connector, then link the SLT Connector to the Cluster Table Splitter operator, and finally create an output port named `bseg`.



> ### Note:  
> If there are special characters like `_` or `/` in the logical table names, remove these when creating the additional output port. For example, logical table `EXAMPLE_TABLE` should be mapped to port `exampletable`, and `/1LT/EXAMPLE` to `1ltexample`



<a name="loioaefc6b9f14b84942989df550a81faa07__section_szc_kpv_zkb"/>

## General Concepts

The following general concepts are relevant for this operator:

-   Authorizations

-   Versioning


For a description of these concepts, see [ABAP Operators General Concepts](abap-operators-general-concepts-bde149c.md).



<a name="loioaefc6b9f14b84942989df550a81faa07__section_bwp_s5b_snb"/>

## New Features

As of V2, the output type for this operator has changed from `abap.*` to `message`.



<a name="loioaefc6b9f14b84942989df550a81faa07__section_sqr_jn2_djb"/>

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
<th valign="top">

Relevant in Version

</th>
</tr>
<tr>
<td valign="top">

ABAP Connection

</td>
<td valign="top">

connectionID

</td>
<td valign="top">

string

</td>
<td valign="top">

Mandatory. The connection information for the remote ABAP system. You can select a predefined ABAP connection from the Connection Manager.

Default: ""

</td>
<td valign="top">

V0, V1, V2

</td>
</tr>
<tr>
<td valign="top">

Version

</td>
<td valign="top">

operatorID

</td>
<td valign="top">

string

</td>
<td valign="top">

The specific version of the operator.

Default: ""

</td>
<td valign="top">

V1, V2

</td>
</tr>
</table>



<a name="loioaefc6b9f14b84942989df550a81faa07__section_u35_33c_xdb"/>

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

in

</td>
<td valign="top">

`abap.*` for V0 and V1 and `message` as of V2

</td>
<td valign="top">

SLT Connector transfers all the logical tables data into Cluster Table Splitter.

</td>
</tr>
</table>



<a name="loioaefc6b9f14b84942989df550a81faa07__section_jxw_y3c_xdb"/>

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

<output port name\>

</td>
<td valign="top">

`abap.*` for V0 and V1 and `message` as of V2

</td>
<td valign="top">

Create one output port for each relevant logical table, using the table name as the port name.

</td>
</tr>
</table>

