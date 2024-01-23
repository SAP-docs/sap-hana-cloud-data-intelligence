<!-- loiob5a8a6072337433ebdc1145887ade880 -->

# LPAD

Use the LPAD function to pad the start of a given string with spaces to make a string of `n` characters in length.



<a name="loiob5a8a6072337433ebdc1145887ade880__section_uyh_41y_s4b"/>

## Syntax

<code>LPAD(<i class="varname">&lt;string&gt;</i>, <i class="varname">&lt;n&gt;</i> [, <i class="varname">&lt;pattern&gt;</i>])</code> 



<a name="loiob5a8a6072337433ebdc1145887ade880__section_vyh_41y_s4b"/>

## Description

Given a string, and the length of the output string, the LPAD function pads the start of the string with spaces to make a string of `n` characters in length. Use the <code><i class="varname">&lt;pattern&gt;</i></code> argument to pad the given string using sequences of the <code><i class="varname">&lt;pattern&gt;</i></code> until the required length is met.



> ### Example:  
> The following examples illustrate how the LPAD function works:
> 
> -   The following function returns the string `123451234512end`: `LPAD(‘end’, 15, ‘12345’)`
> 
>     The function left pads the start of the string, `end`, with the pattern `12345` to make a string of `15` characters in length.
> 
> -   The following function returns the string `en`: `LPAD(‘end’, 2, ‘12345’)`
> 
>     The given string, `end`, is longer than the specified string length of `2`. Therefore, the function doesn't add the pattern `12345` as padding, and the resulting string is truncated to the length of two characters.

