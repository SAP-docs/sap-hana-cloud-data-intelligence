<!-- loiod7966c712a904db88f76e36ef6fddec0 -->

# Flowagent File Consumer \(Deprecated\)

This operator reads from any supported cloud storage or local file.



It uses Flowagent subengine for execution, and you need to connect it to a Flowagent-based producer operator \(e.g. Flowagent CSV Producer\).

> ### Caution:  
> Support for Azure Data Lake Gen1 \(ADL\) in this operator is deprecated.



<a name="loiod7966c712a904db88f76e36ef6fddec0__section_lsl_q5p_1xb"/>

## Supported Cloud Storage

-   Azure Data Lake V2 \(ADL\_V2\)
-   Google Cloud Storage \(GCS\)
-   HDFS
-   SAP HANA Data Lake Files \(HDL\_FILES\)
-   Amazon S3 \(S3\)
-   Windows Azure Storage Blob \(WASB\)
-   Semantic Data Lake \(SDL\)
-   Alibaba OSS \(OSS\)
-   Local



<a name="loiod7966c712a904db88f76e36ef6fddec0__section_hgl_2p2_p2b"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Parameter

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

Storage type

</td>
<td valign="top">

string

</td>
<td valign="top">

The storage from which the file be will read. Additional parameters may depend on the selected cloud storage.

</td>
</tr>
<tr>
<td valign="top">

ADL V2 Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Object containing the connection parameters to an ADL V2 remote.

</td>
</tr>
<tr>
<td valign="top">

SDL Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Object containing the connection parameters to a SDL remote.

</td>
</tr>
<tr>
<td valign="top">

HDFS Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Object containing the connection parameters to a HDFS remote.

</td>
</tr>
<tr>
<td valign="top">

HDL FILES Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Object containing the connection parameters to a HDL\_FILES remote.

</td>
</tr>
<tr>
<td valign="top">

GCS Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Object containing the connection parameters to a GCS remote.

</td>
</tr>
<tr>
<td valign="top">

S3 Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Object containing the connection parameters to a S3 remote.

</td>
</tr>
<tr>
<td valign="top">

OSS Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Object containing the connection parameters to an Alibaba OSS remote.

</td>
</tr>
<tr>
<td valign="top">

WASB Connection

</td>
<td valign="top">

object

</td>
<td valign="top">

Object containing the connection parameters to a WASB remote.

</td>
</tr>
<tr>
<td valign="top">

ADL V2 file name

</td>
<td valign="top">

object

</td>
<td valign="top">

Full path to the file which will be read in the storage.

</td>
</tr>
<tr>
<td valign="top">

SDL file name

</td>
<td valign="top">

object

</td>
<td valign="top">

Full path to the file which will be read in the storage.

</td>
</tr>
<tr>
<td valign="top">

HDFS file name

</td>
<td valign="top">

object

</td>
<td valign="top">

Full path to the file which will be read in the storage.

</td>
</tr>
<tr>
<td valign="top">

HDL FILES file name

</td>
<td valign="top">

object

</td>
<td valign="top">

Full path to the file which will be read in the storage.

</td>
</tr>
<tr>
<td valign="top">

GCS file name

</td>
<td valign="top">

object

</td>
<td valign="top">

Full path to the file which will be read in the storage.

</td>
</tr>
<tr>
<td valign="top">

S3 file name

</td>
<td valign="top">

object

</td>
<td valign="top">

Full path to the file which will be read in the storage.

</td>
</tr>
<tr>
<td valign="top">

OSS file name

</td>
<td valign="top">

object

</td>
<td valign="top">

Full path to the file that is read in the storage.

</td>
</tr>
<tr>
<td valign="top">

WASB file name

</td>
<td valign="top">

object

</td>
<td valign="top">

Full path to the file which will be read in the storage.

</td>
</tr>
<tr>
<td valign="top">

Local file name

</td>
<td valign="top">

string

</td>
<td valign="top">

Full path to the file which will be read from local storage.

</td>
</tr>
<tr>
<td valign="top">

Fail on string truncation

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Indicates if the reader should exit and fail if a string truncation has happened. This can happen if the length of a string in the metadata is smaller than the actual data in the source file. This option does not apply to ‘local’ storage type and behavior will default to False and data will be truncated.

</td>
</tr>
<tr>
<td valign="top">

Fetch Size

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the number of rows fetched from the source in each request. For wide files, smaller values are better. For files with less columns, larger values are better.

</td>
</tr>
<tr>
<td valign="top">

Select random sample

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Indicates whether the reader should read the full file or a random sample of records from the source. If set to true, then the ‘Number of sample rows’ parameter is used to determine the maximum number of random records selected.

</td>
</tr>
<tr>
<td valign="top">

Number of sample rows

</td>
<td valign="top">

integer

</td>
<td valign="top">

Indicates the maximum number of random sample records to read from the source.

</td>
</tr>
</table>



<a name="loiod7966c712a904db88f76e36ef6fddec0__section_lzv_rwp_1xb"/>

## Remote source description limitation

When you select a file to be read via the browsing UI, it will obtain the metadata definition for the file. There are three major limitations with this approach:

1.  CSV files do not have metadata definition, so it will infer the metadata by looking at the file.
2.  Parquet and ORC files have metadata definition, but they do not specify the length of strings, which here are defaulted to 5000.
3.  For ‘local’ sources, browsing and selection is not supported and the metadata definition will not be generated.

Given these facts, the metadata can be wrong, and the job may fail. For strings, the default is to fail the job on strings truncation; however, it can be configured to tolerate string truncations by setting the *Fail on string truncation* property to *false*. For ‘local’ storage type, the behavior is always false and the string data will simply be truncated.



<a name="loiod7966c712a904db88f76e36ef6fddec0__section_r4f_lrx_dlb"/>

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

inFileName

</td>
<td valign="top">

string

</td>
<td valign="top">

Remote file name.

> ### Note:  
> Input port is optional, and the value of this is over-ridden by value from Operator Configuration, hence can be used as trigger as well.



</td>
</tr>
</table>



<a name="loiod7966c712a904db88f76e36ef6fddec0__section_g1c_hsx_dlb"/>

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

outConfig

</td>
<td valign="top">

string.flowagent.config

</td>
<td valign="top">

Flowagent type port, which only Flowagent producers can consume \(for example, Flowagent File Producer\). To get the data as string, Flowagent CSV Producer can be used as producer.

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

