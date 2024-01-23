<!-- loioe81bd114b4df4295ba2dbe9634c5c1af -->

# Data Type Compatibility

SAP Data Intelligence replication flow maintains data type compatibility between source and target data types.



The following table specifies compatible data types so that you choose a compatible data type when you create a replication flow.



<a name="loioe81bd114b4df4295ba2dbe9634c5c1af__section_ydf_j32_gyb"/>

## Replication Management Service Data Type Compatibility


<table>
<tr>
<th valign="top">

Source Data Type

</th>
<th valign="top">

Compatible Target Data Type

</th>
<th valign="top">

Additional Information

</th>
</tr>
<tr>
<td valign="top">

uint8

</td>
<td valign="top">

uint8  
 int16  
 int32  
 int64  
 uint64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

int8

</td>
<td valign="top">

int8  
 int16  
 int32  
 int64  


</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

int16

</td>
<td valign="top">

int16  
 int32  
 int64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

int32

</td>
<td valign="top">

int32  
 int64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

int64

</td>
<td valign="top">

int64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

uint64

</td>
<td valign="top">

uint64  
 decimal \(p,s\)

</td>
<td valign="top">

decimal\(p,s\), where \(p − s\) \>= 20.

</td>
</tr>
<tr>
<td valign="top">

bool

</td>
<td valign="top">

bool  
 uint8  
 int8  
 int16  
 int32  
 int64  


</td>
<td valign="top">

For int and uint data types:

-   true = 1
-   false = 0



</td>
</tr>
<tr>
<td valign="top">

decfloat16

</td>
<td valign="top">

decfloat16  
 decfloat34

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

decfloat34

</td>
<td valign="top">

decfloat34

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

float32

</td>
<td valign="top">

float32  
 float64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

float64

</td>
<td valign="top">

float64

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

date

</td>
<td valign="top">

date

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

time

</td>
<td valign="top">

time

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

timestamp

</td>
<td valign="top">

timestamp

</td>
<td valign="top">

N/A

</td>
</tr>
<tr>
<td valign="top">

decimal \(p,s\)

</td>
<td valign="top">

decimal \(p,s\)

</td>
<td valign="top">

Verify length, precision \(p\), and scale \(s\):

-   Target length must be \>= source length.
-   Target s must be \>= source s.
-   Target \(p − s\) must be \>= source \(p − s\).



</td>
</tr>
<tr>
<td valign="top">

string\(n\)

</td>
<td valign="top">

string\(m\)

</td>
<td valign="top">

m \>= n

</td>
</tr>
<tr>
<td valign="top">

binary\(n\)

</td>
<td valign="top">

binary\(n\)

</td>
<td valign="top">

Target length must be \>= source length.

</td>
</tr>
</table>

