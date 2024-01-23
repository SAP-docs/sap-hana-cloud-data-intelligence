<!-- loio75bf127f199842c6a7334773c6cef87e -->

# SUBSTRING

The SUBSTRING function returns a substring of the given string starting at the `start_position` in the string.



<a name="loio75bf127f199842c6a7334773c6cef87e__section_xzb_rdy_s4b"/>

## Syntax

<code>SUBSTRING(<i class="varname">&lt;string&gt;</i>, <i class="varname">&lt;start_position&gt;</i> [, <i class="varname">&lt;string_length&gt;</i>])</code> 



<a name="loio75bf127f199842c6a7334773c6cef87e__section_yzb_rdy_s4b"/>

## Description

When provided with a string and a start position, the SUBSTRING function returns a substring of the given string. SUBSTRING returns the remaining part of a string starting at the <code><i class="varname">&lt;start_position&gt;</i></code>. If you specify a length in <code><i class="varname">&lt;string_length&gt;</i></code>, SUBSTRING returns a string that is as long as the set string length. The following list describes how the SUBSTRING function works under specific situations:

-   If <code><i class="varname">&lt;start_position&gt;</i></code> is less than 1, the SUBSTRING function considers it a 1.
-   If <code><i class="varname">&lt;string_length&gt;</i></code> is less than 1, then the SUBSTRING function returns an empty string.
-   If <code><i class="varname">&lt;string_length&gt;</i></code> is greater than the length of the remaining part of the string, then the SUBSTRING function returns the remaining part of the string without padding the string with blanks.



> ### Example:  
> -   The following function returns the value `45`: `SUBSTRING(‘1234567890’, 4, 2)`. SUBSTRING selects two characters from the given string starting with the fourth character.
> 
> -   The following function returns the value `‘ABCD’` from the binary value `x'ABCDEF'`: `SUBSTRING(x’ABCDEF’, 1, 2)`.

