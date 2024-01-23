<!-- loio575ffd386d6d1014b3fc9283b0e91070 -->

# abs

Use the abs function to return the absolute value of a number. The absolute value \(sometimes known as the modulus\) of a number is the value of a number without regard to its sign – it can also be thought of as the distance of a number from zero.



This topic applies to SAP Data Intelligence.



```
abs(<num>)
```



## Return value

decimal, double, int, or real

The absolute value of the given number, *<num\>*. The type of the return value is the same as the type of the original number.



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
> abs(12.12345)
> 
> ```
> 
> 
> 
> </td>
> <td valign="top">
> 
> ```
> 12.12345
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
> abs(-12.12345)
> 
> ```
> 
> 
> 
> </td>
> <td valign="top">
> 
> ```
> 12.12345
> 
> ```
> 
> 
> 
> </td>
> </tr>
> </table>

