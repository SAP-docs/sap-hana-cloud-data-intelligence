<!-- loio9ef2c5d8b3c1427bb90ff1108f8efbf3 -->

# ADD\_DAYS

The ADD\_DAYS function returns a date when given a date and additional number of days.



<a name="loio9ef2c5d8b3c1427bb90ff1108f8efbf3__section_brl_qlh_bpb"/>

## Syntax

<code>ADD_DAYS(<i class="varname">&lt;date&gt;</i>, <i class="varname">&lt;n&gt;</i>)</code> 



<a name="loio9ef2c5d8b3c1427bb90ff1108f8efbf3__section_crl_qlh_bpb"/>

## Description

The ADD\_DAYS function adds the given number of days in <code><i class="varname">&lt;n&gt;</i></code> to a given date in <code><i class="varname">&lt;date&gt;</i></code> and returns a new date.



> ### Example:  
> The following function results in `2010-01-04`: `ADD_DAYS(TO_DATE(‘2009-12-05’, ‘yyyy-MM-dd’), 30)`.
> 
> The function increments the date value `2009-12-05` by `30` days and uses the given date format for the return value.
> 
> > ### Note:  
> > TO\_DATE converts a date string to a date data type.

