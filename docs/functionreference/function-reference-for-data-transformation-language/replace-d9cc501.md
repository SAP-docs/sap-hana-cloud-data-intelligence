<!-- loiod9cc50188ebf4a218aa96775b1eeb6b2 -->

# REPLACE

The REPLACE function searches a given string for all occurrences of a search string. It then replaces the search string with a given replacement string.



<a name="loiod9cc50188ebf4a218aa96775b1eeb6b2__section_tsk_mby_s4b"/>

## Syntax

<code>REPLACE(<i class="varname">&lt;original_string&gt;</i>, <i class="varname">&lt;search_string&gt;</i>, <i class="varname">&lt;replace_string&gt;</i>)</code> 



<a name="loiod9cc50188ebf4a218aa96775b1eeb6b2__section_usk_mby_s4b"/>

## Description

When given a string, the REPLACE function searches the string for a given search string, and replaces the search string with a replacement string. The following lists special circumstances for the REPLACE function:

-   If the <code><i class="varname">&lt;original_string&gt;</i></code> is empty, the function returns an empty string.
-   If two overlapping substrings match the <code><i class="varname">&lt;search_string&gt;</i></code> in the <code><i class="varname">&lt;original_string&gt;</i></code>, then the function replaces only the first occurrence.
-   If the <code><i class="varname">&lt;original_string&gt;</i></code> doesn't contain any occurrence of the <code><i class="varname">&lt;search_string&gt;</i></code>, then the function returns the <code><i class="varname">&lt;original_string&gt;</i></code>.
-   If the <code><i class="varname">&lt;original_string&gt;</i></code>, <code><i class="varname">&lt;search_string&gt;</i></code>, or <code><i class="varname">&lt;replace_string&gt;</i></code> are NULL, then the function returns NULL.



> ### Example:  
> The following function returns `UPGRADE UPWARD`: `REPLACE(‘DOWNGRADE DOWNWARD’,’DOWN’, ‘UP’)`
> 
> This function replaces all occurrences of `DOWN` in the original string with `UP`.

