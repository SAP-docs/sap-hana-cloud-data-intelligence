<!-- loiof15018e537f748b4acbbe1cdfdfdcf65 -->

# TRIM

The TRIM function returns the given string after it removes leading and trailing spaces.



<a name="loiof15018e537f748b4acbbe1cdfdfdcf65__section_wkp_c2y_s4b"/>

## Syntax

<code>TRIM([{LEADING | TRAILING | BOTH} <i class="varname">&lt;trim_char&gt;</i> FROM] <i class="varname">&lt;string&gt;</i>)</code>



<a name="loiof15018e537f748b4acbbe1cdfdfdcf65__section_xkp_c2y_s4b"/>

## Description

The TRIM function removes leading and trailing spaces from a given string. The trim operation works from the start \(LEADING\), end \(TRAILING\) or both \(BOTH\) ends of the string. The following list describes how the TRIM function works under specific situations:

-   If either <code><i class="varname">&lt;string&gt;</i></code> or <code><i class="varname">&lt;trim_char&gt;</i></code> is NULL, then TRIM returns NULL.
-   If no options are specified, TRIM removes both the leading and trailing substring specified in <code><i class="varname">&lt;trim_char&gt;</i></code> from the given string.
-   If <code><i class="varname">&lt;trim_char&gt;</i></code> isn't specified, then TRIM uses a single blank space.



> ### Example:  
> -   The following function removes all leading and trailing “`a`” characters from the string and returns `123456789`: `TRIM(‘a’ FROM ‘aaa123456789aa’)`.
> 
> -   The following function removes the character “`a`” at the beginning \(`LEADING`\) of the string and returns `123456789aa`: `TRIM(LEADING ‘a’ FROM ‘aaa123456789aa’)`.

