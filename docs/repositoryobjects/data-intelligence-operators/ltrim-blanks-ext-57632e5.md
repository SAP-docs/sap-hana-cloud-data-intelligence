<!-- loio57632e526d6d1014b3fc9283b0e91070 -->

# ltrim\_blanks\_ext

Use the ltrim\_blanks\_ext function to remove blank and control characters from the start of a string.



This topic applies to SAP Data Intelligence.



```
ltrim_blanks_ext(<input_string>)

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



<a name="loio57632e526d6d1014b3fc9283b0e91070__section_s1g_szx_vdb"/>

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
> `ltrim_blanks_ext(' Marilyn')`
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
> `ltrim_blanks_ext(last_name)`
> 
> </td>
> <td valign="top">
> 
> The value contained in the column last\_name, with all leading blanks and control characters removed.
> 
> </td>
> </tr>
> </table>



