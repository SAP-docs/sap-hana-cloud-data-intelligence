<!-- loio40e5f8dd567d4b71ba11d59ef9105b25 -->

# Batch Header

Operators use batch headers to express information about its output batches in a unified way.

The batch header consists of the following elements:

-   **Kind:** `structure`
-   **Type ID:** `com.sap.headers.batch`

The following table describes the batch header fields.


<table>
<tr>
<th valign="top">

Field

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`index`

</td>
<td valign="top">

Integer with the zero-based index of the batch.

</td>
</tr>
<tr>
<td valign="top">

`isLast`

</td>
<td valign="top">

Boolean that indicates whether the batch is the last in the sequence, for example, `if batchIndex == batchCount-1`.

</td>
</tr>
<tr>
<td valign="top">

`count`

</td>
<td valign="top">

Total number of batches in the sequence. If the operator can't obtain the `count` because of technical restrictions or because the sequence is open-ended \(a stream\), for example, operators can omit `count`.

</td>
</tr>
<tr>
<td valign="top">

`size`

</td>
<td valign="top">

Number indicating the magnitude that delimits one batch from the next. For example, the number of bytes or the number of lines of text the batch contains. When you use other criteria, such as a timeout for the accumulation of each batch, you can omit `size`.

`Size` doesn't express the size of an individual batch. Rather, `size` expresses the intended size for batches in general. Size is usually specified by the user.

</td>
</tr>
<tr>
<td valign="top">

`unit`

</td>
<td valign="top">

String containing the unit in which `batchSize` is measured. If present, `unit` is expressed as one of the following measures:

-   `bytes`.
-   `rows`, for table-related operators \(including CSV, databases, and so on\).
-   `lines`, for text files.



</td>
</tr>
</table>



<a name="loio40e5f8dd567d4b71ba11d59ef9105b25__section_tjg_nsn_bsb"/>

## Example

> ### Example:  
> You configure a Read File operator to read files in 10-byte chunks. If the file has a total of 87 bytes, the operator outputs the following values for the batch attributes:
> 
> -   `index` in the range \[0,8\]
> -   `isLast`: false in all but the ninth and last output \(index 8\)
> -   `count`: 9
> -   `size`: 10
> -   `unit`: bytes

