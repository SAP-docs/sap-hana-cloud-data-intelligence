<!-- loio27ac4e462f434d21968213958d022de3 -->

# RIGHT

The RIGHT function returns the rightmost characters or bytes of the given string based on the specified number of characters.



<a name="loio27ac4e462f434d21968213958d022de3__section_vpt_wby_s4b"/>

## Syntax

<code>RIGHT(<i class="varname">&lt;string&gt;</i>, <i class="varname">&lt;n&gt;</i>)</code> 



<a name="loio27ac4e462f434d21968213958d022de3__section_wpt_wby_s4b"/>

## Description

When given a string, the RIGHT function returns the rightmost characters or bytes in the string, the length of which is set in <code><i class="varname">&lt;n&gt;</i></code>. The following list describes how the RIGHT function works under specific situations:

-   If the value of <code><i class="varname">&lt;n&gt;</i></code> is less than 1, RIGHT returns an empty string value.
-   If the value of <code><i class="varname">&lt;n&gt;</i></code> is greater than the length of <code><i class="varname">&lt;string&gt;</i></code>, the function returns the string without padding with blank spaces.



> ### Example:  
> -   The following function returns `789`: `RIGHT(‘HI0123456789’, 3)`.
> 
> -   The following function returns `HI0123456789`, because the value `20` exceeds the length of the input string: `RIGHT(‘HI0123456789’, 20)`.

