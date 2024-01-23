<!-- loiof76cf4a0381749b4991d5d23402d7072 -->

# ADD\_YEARS

The ADD\_YEARS function returns a new date by adding a given number of years to a given date.



<a name="loiof76cf4a0381749b4991d5d23402d7072__section_hyg_smh_bpb"/>

## Syntax

<code>ADD_YEARS(<i class="varname">&lt;date&gt;</i>, <i class="varname">&lt;n&gt;</i>)</code> 



<a name="loiof76cf4a0381749b4991d5d23402d7072__section_iyg_smh_bpb"/>

## Description

The ADD\_YEARS function adds the given number of years in <code><i class="varname">&lt;n&gt;</i></code> to a given date in <code><i class="varname">&lt;date&gt;</i></code> and returns a new date.



> ### Example:  
> The following function returns `2010-12-05`: `ADD_YEARS(TO_DATE(‘2009-12-05’, ‘yyyy-MM-dd’), 1)`

This function increments the date value `2009-12-05` by `1` year.

> ### Note:  
> TO\_DATE converts a date string to a date data type.

