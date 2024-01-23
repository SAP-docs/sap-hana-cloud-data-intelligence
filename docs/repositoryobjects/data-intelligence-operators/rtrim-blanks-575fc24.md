<!-- loio575fc2496d6d1014b3fc9283b0e91070 -->

# rtrim\_blanks

Use the rtrim\_blanks function to remove blank characters from the end of a string.



This topic applies to SAP Data Intelligence.



```
rtrim_blanks(<input_string>)

```



## Return value

varchar

The modified string. The return type is the same as *<input\_string\>*.



## Where


<table>
<tr>
<td valign="top">

*<input\_string\>* 

</td>
<td valign="top">

The string to be modified.

</td>
</tr>
</table>



<a name="loio575fc2496d6d1014b3fc9283b0e91070__section_jqw_m22_wdb"/>

## Details

If the length of the modified string becomes zero after trimming, the function returns '' \(empty string\).

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
> `rtrim_blanks('Marilyn ')` 
> 
> </td>
> <td valign="top">
> 
> 'Marilyn'
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> `rtrim_blanks(last_name)` 
> 
> </td>
> <td valign="top">
> 
> The value contained in the column `last_name` with trailing blanks removed.
> 
> </td>
> </tr>
> </table>

