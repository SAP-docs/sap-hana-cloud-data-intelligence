<!-- loio07d92a2e8e7b4c128360f59ddee088ba -->

# ADD\_SECONDS

The ADD\_SECONDS function returns a new time by adding a given number of seconds to a given time.



<a name="loio07d92a2e8e7b4c128360f59ddee088ba__section_qhk_lmh_bpb"/>

## Syntax

<code>ADD_SECONDS(<i class="varname">&lt;time&gt;</i>, <i class="varname">&lt;n&gt;</i>)</code> 



<a name="loio07d92a2e8e7b4c128360f59ddee088ba__section_rhk_lmh_bpb"/>

## Description

The ADD\_SECONDS function adds the given number of seconds in <code><i class="varname">&lt;n&gt;</i></code> to a given time in <code><i class="varname">&lt;time&gt;</i></code> and returns a new time.



> ### Example:  
> The following function returns `2012-01-02 00:00:45`: `ADD_SECONDS(TO_DATETIME(‘2012-01-01 23:30:45’, ‘yyyy-MM-dd HH:mm:ss’), 60 30)`.
> 
> The function increments the DATETIME value `2012-01-01 23:30:45` by `60 30` seconds and returns the value in the provided format.
> 
> > ### Note:  
> > TO\_DATETIME converts a date string to a datetime data type.

