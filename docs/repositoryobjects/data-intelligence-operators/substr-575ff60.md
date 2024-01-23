<!-- loio575ff6036d6d1014b3fc9283b0e91070 -->

# substr

Use the substr function to return a specific portion of a string starting at a given point in the string.



```
substr(<input_string>, <start>, <length>)

```



## Return value

varchar

The modified string. The return data type is the *<input\_string\>*. If the length is a constant, then it is a varchar of the given length.



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

*<start\>* 

</td>
<td valign="top">

The position in the *<input\_string\>* where the function obtains the first character of the new string. The function counts characters from the beginning of *<input\_string\>*.

-   In normal data flows, the first character is position number 1.
-   If *<start\>* is 0, the new string begins with the first character \(position 1\).
-   If *<start\>* is negative, the function counts characters from the end of *<input\_string\>*.

The new string begins with the character in that position from the end of the string. The function returns NULL or an empty string under the following circumstances:

-   If *<start\>* is greater than the number of characters in *<input\_string\>*, the function returns NULL.
-   If *<length\>* is less than 1, the function returns an empty string.



</td>
</tr>
<tr>
<td valign="top">

*<length\>* 

</td>
<td valign="top">

The number of characters in the resulting string.

-   If *<length\>* is 0 or negative, the function returns an empty string.
-   If *<length\>* is greater than the number of characters remaining in *<input\_string\>* after *<start\>* , the function returns only the remaining characters.

The function keeps the trailing blanks in the remaining *<input\_string\>* after *<start\>*.

</td>
</tr>
</table>

For information about how Data Services uses the substr function with HANA, see SAP Note [2808903](https://me.sap.com/notes/2808903).



<a name="loio575ff6036d6d1014b3fc9283b0e91070__section_q3y_zq1_xdb"/>

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
> `substr('94025-3373', 1, 5)`
> 
> </td>
> <td valign="top">
> 
> '94025'
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> `substr('94025-3373', 7, 4)`
> 
> </td>
> <td valign="top">
> 
> '3373'
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> `substr('94025', 7, 4)`
> 
> </td>
> <td valign="top">
> 
> NULL
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> `substr('Dr. Schultz', 4, 18)`
> 
> </td>
> <td valign="top">
> 
> 'Schultz'
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> `substr('San Francisco, CA',-4, 18)`
> 
> </td>
> <td valign="top">
> 
> ', CA'
> 
> </td>
> </tr>
> </table>

