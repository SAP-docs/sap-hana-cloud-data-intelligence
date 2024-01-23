<!-- loioc70045273f5642c99c6eb3ffe99dcd4b -->

# ADD\_MONTHS

The ADD\_MONTHS function returns a date when given a date and a number of months.



<a name="loioc70045273f5642c99c6eb3ffe99dcd4b__section_p5f_2mh_bpb"/>

## Syntax

<code>ADD_MONTHS(<i class="varname">&lt;date&gt;</i>, <i class="varname">&lt;n&gt;</i>)</code> 



<a name="loioc70045273f5642c99c6eb3ffe99dcd4b__section_q5f_2mh_bpb"/>

## Description

The ADD\_MONTHS function adds the given number of months in <code><i class="varname">&lt;n&gt;</i></code> to a given date in <code><i class="varname">&lt;date&gt;</i></code> and returns a new date.



> ### Example:  
> The following function returns `2010-01-05`: `ADD_MONTHS(TO_DATE(‘2009-12-05’, ‘yyyy-MM-dd’), 1)`.
> 
> The function increments the date value `2009-12-05` by `1` month and returns a new date using the given date format.

