<!-- loio575fbb306d6d1014b3fc9283b0e91070 -->

# rtrim

Use the rtrim function to remove specified characters from the end of a string.



This topic applies to SAP Data Intelligence.



```
rtrim('<input_string>', '<trim_string>')

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
<tr>
<td valign="top">

*<trim\_string\>* 

</td>
<td valign="top">

The characters to remove from *<input\_string\>*.

</td>
</tr>
</table>



<a name="loio575fbb306d6d1014b3fc9283b0e91070__section_bkh_222_wdb"/>

## Details

The function scans *<input\_string\>* from right to left removing all characters that appear in *<trim\_string\>* until it reaches a character not in *<trim\_string\>*.

Removes trailing blanks only if *<trim\_string\>* contains trailing blanks. If the length of the modified string becomes zero after trimming, the function returns '' \(empty string\).

To remove all trailing blanks in a string, use the rtrim\_blanks function.

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
> `rtrim('Marilyn ', ' ')` 
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
> `rtrim('ZABCABC', 'ABC')` 
> 
> </td>
> <td valign="top">
> 
> 'Z'
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> `rtrim('ZABCABC', 'EFG')` 
> 
> </td>
> <td valign="top">
> 
> 'ZABCABC'
> 
> </td>
> </tr>
> </table>
> 
> You may also use the rtrim\_blanks or rtrim\_blanks\_ext functions for this.

