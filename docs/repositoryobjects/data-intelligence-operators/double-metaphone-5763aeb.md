<!-- loio5763aeb26d6d1014b3fc9283b0e91070 -->

# double\_metaphone

Use the double\_metaphone function to encode the input string using the Double Metaphone algorithm.



This topic applies to SAP Data Intelligence.



```
double_metaphone(<input_str, alternate, return_if_empty>)
```



## Return Value

varchar

Returns the string containing the double metaphone encoding of the input string. The length of the return string depends on the length of the input string, but it is always shorter than the input string.



## Where


<table>
<tr>
<td valign="top">

*<input\_str\>* 

</td>
<td valign="top">

The source string to encode.

</td>
</tr>
<tr>
<td valign="top">

*<alternate\>* 

</td>
<td valign="top">

A flag to control how the function returns the encoded strings.

-   When 0, returns the primary encoding. When no primary encoding, returns NULL or the input string based on how you set *<return\_if\_empty\>*.
-   When input is not 0, returns the alternate encoding. If no alternate encoding, returns NULL or the input string based on how you set *<return\_if\_empty\>*.
-   When NULL or invalid, such as non numeric, defaults to 0.



</td>
</tr>
<tr>
<td valign="top">

*<return\_if\_empty\>* 

</td>
<td valign="top">

A flag to determine whether to return null or the input string when there is no encoding.

When 0, return NULL. Otherwise, return the input string when there is no encoding. When the parameter is NULL or invalid, such as non numeric, defaults to 1.

When input is empty, there is no primary or secondary encodings. When *<return\_if\_empty\>* = 0, then returns NULL. When *<return\_if\_empty\>* = 1, then returns the empty string.

</td>
</tr>
</table>



## Details

Only use this function for input strings in English. The function ignores non-English characters.

When input is NULL, the function returns NULL.

When the second or third parameter has an invalid value, defaults to 0 and 1, respectively.

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
> Result
> 
> </th>
> </tr>
> <tr>
> <td valign="top">
> 
> ```
> Print(double_metaphone('Hello',0,0);
> 
> ```
> 
> 
> 
> </td>
> <td valign="top">
> 
> Prints the double metaphone of the word “Hello.” 
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> ```
> double_metaphone($VAR, 1,1);
> ```
> 
> 
> 
> </td>
> <td valign="top">
> 
> If the string stored in $VAR does not have encoding available, then returns the original string.
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> ```
> double_metaphone($VAR,'a','b');
> ```
> 
> 
> 
> </td>
> <td valign="top">
> 
> Returns the primary double metaphone encoding or the variable $VAR when the primary encoding does not exist.
> 
> </td>
> </tr>
> </table>

