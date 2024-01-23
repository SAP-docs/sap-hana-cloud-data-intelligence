<!-- loiobd4523a7b1e249af95657146edd392e3 -->

# LEFT

The LEFT function returns the first `n` characters or bytes from the beginning of a string.



<a name="loiobd4523a7b1e249af95657146edd392e3__section_rnx_jrx_s4b"/>

## Syntax

<code>LEFT(<i class="varname">&lt;string&gt;</i>, <i class="varname">&lt;n&gt;</i>)</code>



<a name="loiobd4523a7b1e249af95657146edd392e3__section_snx_jrx_s4b"/>

## Description

When given a string and a number that represents the number of characters to return, the LEFT function returns the first <code><i class="varname">&lt;n&gt;</i></code> characters or bytes from the beginning of the given string. The following are special circumstances for the LEFT function:

-   Returns an empty string when <code><i class="varname">&lt;n&gt;</i></code> is less than 1.

-   Returns the entire <code><i class="varname">&lt;string&gt;</i></code> without blank padding when the value of <code><i class="varname">&lt;n&gt;</i></code> is greater than the length of given string.




> ### Example:  
> The following function returns `Hel`: `LEFT(‘Hello’, 3)`.
> 
> The following function returns the entire string, `Hello`, because the value `10` exceeds the given string length: `LEFT(‘Hello’, 10)`.

