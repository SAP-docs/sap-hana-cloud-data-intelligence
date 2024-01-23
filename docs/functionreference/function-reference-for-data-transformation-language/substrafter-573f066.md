<!-- loio573f066bda3a49508dc8b42a925fdbf8 -->

# SUBSTRAFTER

The SUBSTRAFTER function returns a substring of a given string that follows the first occurrence of characters in the <code><i class="varname">&lt;pattern&gt;</i></code> argument.



<a name="loio573f066bda3a49508dc8b42a925fdbf8__section_utd_bdy_s4b"/>

## Syntax

<code>SUBSTR_AFTER(<i class="varname">&lt;string&gt;</i>, <i class="varname">&lt;pattern&gt;</i>)</code> 



<a name="loio573f066bda3a49508dc8b42a925fdbf8__section_vtd_bdy_s4b"/>

## Description

When given a pattern, the SUBSTRAFTER function returns a substring of the given string that follows the first occurrence of the pattern. The following list describes how the SUBSTRAFTER function works under specific situations:

-   If <code><i class="varname">&lt;string&gt;</i></code> doesn't contain the <code><i class="varname">&lt;pattern&gt;</i></code> substring, then SUBSTRAFTER returns an empty string.
-   If <code><i class="varname">&lt;pattern&gt;</i></code> is an empty string, then SUBSTRAFTER returns the <code><i class="varname">&lt;string&gt;</i></code>.
-   If <code><i class="varname">&lt;string&gt;</i></code> or <code><i class="varname">&lt;pattern&gt;</i></code> is NULL, then SUBSTRAFTER returns `NULL`.



> ### Example:  
> The following function returns `Friend`: `SUBSTR_AFTER(‘Hello My Friend’,’My‘)`. `Friend` is the part of the given string that is to the right of the first occurrence of `My`.

