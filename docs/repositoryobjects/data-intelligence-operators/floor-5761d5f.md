<!-- loio5761d5ff6d6d1014b3fc9283b0e91070 -->

# floor

Use the floor function to return the largest integer value equal to or less than a number.



This topic applies to SAP Data Intelligence.



```
floor(<num>)
```



## Return value

decimal, double, int, or real

The indicated integer, cast as the same type as the original number, *<num\>* .



## Where


<table>
<tr>
<td valign="top">

*<num\>* 

</td>
<td valign="top">

The source number.

</td>
</tr>
</table>



<a name="loio5761d5ff6d6d1014b3fc9283b0e91070__section_gsj_2hj_vdb"/>

## Details

> ### Example:  
> 
> <table>
> <tr>
> <th valign="top">
> 
> Function
> 
> </th>
> <th valign="top">
> 
> Results
> 
> </th>
> </tr>
> <tr>
> <td valign="top">
> 
> ```
> floor(12.12345)
> 
> ```
> 
> 
> 
> </td>
> <td valign="top">
> 
> ```
> 12.00000
> 
> ```
> 
> 
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> ```
> floor(12)
> 
> ```
> 
> 
> 
> </td>
> <td valign="top">
> 
> ```
> 12
> 
> ```
> 
> 
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> ```
> floor(-12.223)
> 
> ```
> 
> 
> 
> </td>
> <td valign="top">
> 
> ```
> -13.000
> 
> ```
> 
> 
> 
> </td>
> </tr>
> </table>

