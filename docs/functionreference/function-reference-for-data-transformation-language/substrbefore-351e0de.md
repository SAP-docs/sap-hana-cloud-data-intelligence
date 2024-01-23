<!-- loio351e0de2dd40449fb7d6190007061677 -->

# SUBSTRBEFORE

The SUBSTRBEFORE function returns a substring of the given string that precedes the first occurrence of characters in `pattern`.



<a name="loio351e0de2dd40449fb7d6190007061677__section_s5v_gdy_s4b"/>

## Syntax

<code>SUBSTR_BEFORE(<i class="varname">&lt;string&gt;</i>, <i class="varname">&lt;pattern&gt;</i>)</code> 



<a name="loio351e0de2dd40449fb7d6190007061677__section_b24_3dy_s4b"/>

## Description

When given a pattern, the SUBSTRBEFORE function returns a substring of the given string that precedes the first occurrence of the pattern. The following list describes how the SUBSTRBEFORE function works under specific situations:

-   If <code><i class="varname">&lt;string&gt;</i></code> doesn't contain the <code><i class="varname">&lt;pattern&gt;</i></code> substring, then SUBSTRBEFORE returns an empty string.
-   If <code><i class="varname">&lt;pattern&gt;</i></code> is an empty string, then SUBSTRBEFORE returns the <code><i class="varname">&lt;string&gt;</i></code>.
-   If <code><i class="varname">&lt;string&gt;</i></code> or <code><i class="varname">&lt;pattern&gt;</i></code> is NULL, then SUBSTRBEFORE returns `NULL`.



> ### Example:  
> The following function returns `Hello`: `SUBSTR_BEFORE(‘Hello My Friend’,’My’)`. `Hello` is the portion of the given string that is to the left of the first occurrence of `My`.

