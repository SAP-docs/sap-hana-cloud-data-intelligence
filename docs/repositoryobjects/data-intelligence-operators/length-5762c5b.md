<!-- loio5762c5bc6d6d1014b3fc9283b0e91070 -->

# length

Use the length function to return the number of characters in a given string.



This topic applies to SAP Data Intelligence.



```
length(<value>)

```



## Return value

integer

The number of characters in *<value\>*.



## Where


<table>
<tr>
<td valign="top">

*<value\>* 

</td>
<td valign="top">

A string indicating the column name, variable, or other element whose length is calculated.

</td>
</tr>
</table>



<a name="loio5762c5bc6d6d1014b3fc9283b0e91070__section_ijc_4sp_vdb"/>

## Details

> ### Example:  
> In the *Mapping* box of a query, use the length function to return the number of characters in each row of a column. With the OUTPUT field selected in the target schema of a query, enter the following statement in the *Mapping* box:
> 
> ```
> length(dal_emp.ename)
> 
> ```
> 
> The software produces the following results:
> 
> 
> <table>
> <tr>
> <th valign="top">
> 
> Source column \(dal\_emp.ename\)
> 
> </th>
> <th valign="top">
> 
> Target column \(output\)
> 
> </th>
> </tr>
> <tr>
> <td valign="top">
> 
> `jones`
> 
> </td>
> <td valign="top">
> 
> `5` 
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> `nguyen`
> 
> </td>
> <td valign="top">
> 
> `6` 
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> `tanaka`
> 
> </td>
> <td valign="top">
> 
> `6` 
> 
> </td>
> </tr>
> </table>



