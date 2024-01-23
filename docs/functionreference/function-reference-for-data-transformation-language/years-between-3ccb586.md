<!-- loio3ccb586223cb47eeb466363e77a99018 -->

# YEARS\_BETWEEN

YEARS\_BETWEEN function \(Date & Time\) computes the number of years between `date_1` and `date_2`.



<a name="loio3ccb586223cb47eeb466363e77a99018__section_ok5_25h_bpb"/>

## Syntax

`YEARS_BETWEEN(d1, d2)`



<a name="loio3ccb586223cb47eeb466363e77a99018__section_pk5_25h_bpb"/>

## Description

Computes the number of years between `date_1` and `date_2`. Returns NULL if either of `date_1` or `date_2` is NULL.



<a name="loio3ccb586223cb47eeb466363e77a99018__section_qh2_35h_bpb"/>

## Example

1.  `YEARS_BETWEEN(TO_DATE(‘2001-01-01’), TO_DATE(‘2003-03-14’))`

    This example returns the value `2` for the years between the two specified dates.

2.  `YEARS_BETWEEN(TO_DATE(‘2003-10-03’), TO_DATE(‘2001-01-14’))`

    This example returns the value `-2` for the years between the two specified dates.

3.  `YEARS_BETWEEN(TO_DATE(‘2001-10-15’), TO_DATE(‘2003-01-14’))`

    This example returns the value `1` for the years between the two specified dates.

4.  `YEARS_BETWEEN(TO_DATE(‘2001-10-13’), TO_DATE(‘2003-01-14’))`

    This example returns the value `1` for the years between the two specified dates.


