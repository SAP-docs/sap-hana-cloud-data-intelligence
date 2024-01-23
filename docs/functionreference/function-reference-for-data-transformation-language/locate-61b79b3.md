<!-- loio61b79b37465d4dd789308f3eb8cefdae -->

# LOCATE

The LOCATE function returns the position of a search string within a given main string.



<a name="loio61b79b37465d4dd789308f3eb8cefdae__section_yr4_rzx_s4b"/>

## Syntax

<code>LOCATE(<i class="varname">&lt;main_string&gt;</i>, <i class="varname">&lt;search_string&gt;</i> [, start_position])</code>



<a name="loio61b79b37465d4dd789308f3eb8cefdae__section_zr4_rzx_s4b"/>

## Description

When given values in the following arguments, the LOCATE function returns the position of a search string as a number:

-   <code><i class="varname">&lt;main_string&gt;</i></code>: A string of characters.
-   <code><i class="varname">&lt;search_string&gt;</i></code>: A string of characters to locate in the main string.
-   <code><i class="varname">&lt;start_position&gt;</i></code>: Location in the main string in which to start searching for the search string. The <code><i class="varname">&lt;start_position&gt;</i></code> can be a pattern, a number, or can be blank.

The following are special circumstances for the LOCATE function:

-   Returns `0` when <code><i class="varname">&lt;search_string&gt;</i></code> isn't found in <code><i class="varname">&lt;main_string&gt;</i></code>.
-   Returns `NULL` when <code><i class="varname">&lt;search_string&gt;</i></code> or <code><i class="varname">&lt;main_string&gt;</i></code> is NULL, or when <code><i class="varname">&lt;search_string&gt;</i></code> is an empty string.
-   If `start_position` isn't specified or is `0`, the search starts at the beginning of the <code><i class="varname">&lt;main_string&gt;</i></code>.
-   If `start_position` is a negative, the search starts at the end of the <code><i class="varname">&lt;main_string&gt;</i></code>.



> ### Example:  
> -   The following function returns `1`, because the <code><i class="varname">&lt;search_string&gt;</i></code> is empty: `LOCATE(‘length in char’, ‘’)`.
> -   The following function returns `1`, because the search string, `length`, begins in the first position of the main string `length in char`: `LOCATE(‘length in char’, ‘length’)`.
> -   The following function returns `0` because the search string is a pattern, `zchar`, which the function can't find in the main string: `LOCATE(‘length in char’, ‘zchar’)`

