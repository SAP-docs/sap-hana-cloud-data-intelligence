<!-- loio3593ad3ba88349bf870b24fdeadf5041 -->

# EXTRACT

EXTRACT function \(Date & Time\) finds and returns the value of a specified datetime field from date `d`.



<a name="loio3593ad3ba88349bf870b24fdeadf5041__section_iz3_1ph_bpb"/>

## Syntax

`EXTRACT({YEAR | MONTH | DAY | HOUR | MINUTE | SECOND} FROM d)` 



<a name="loio3593ad3ba88349bf870b24fdeadf5041__section_jz3_1ph_bpb"/>

## Description

Finds and returns the value of a specified datetime field from date `d`.



<a name="loio3593ad3ba88349bf870b24fdeadf5041__section_ms1_cph_bpb"/>

## Example

`EXTRACT(YEAR FROM TO_DATETIME(‘2010-01-04 20:30:45’, ‘yyyy-MM-dd HH:mm:ss’))`

This example returns the value `2010` for the year extracted from the specified date.

