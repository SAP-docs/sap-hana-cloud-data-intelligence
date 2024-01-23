<!-- loio86d7e161822641428d03f6abdd5f2131 -->

# MONTHS\_BETWEEN

MONTHS\_BETWEEN function \(Date & Time\) computes the number of months between `date_1` and `date_2`.



<a name="loio86d7e161822641428d03f6abdd5f2131__section_jcj_5rh_bpb"/>

## Syntax

`MONTHS_BETWEEN(d1, d2)`



<a name="loio86d7e161822641428d03f6abdd5f2131__section_kcj_5rh_bpb"/>

## Description

Computes the number of months between `date_1` and `date_2`. Returns NULL if either of `date_1` or `date_2` is NULL.



<a name="loio86d7e161822641428d03f6abdd5f2131__section_fwf_yrh_bpb"/>

## Example

1.  `MONTHS_BETWEEN(TO_DATE(‘2003-01-01’), TO_DATE(‘2003-03-14’))`

    This example returns `2` for the months between the two dates.

2.  `MONTHS_BETWEEN(TO_DATE(‘2003-10-03’), TO_DATE(‘2003-01-14’))`

    This example returns `-8` for the months between the two dates.

3.  `MONTHS_BETWEEN(TO_DATE(‘2003-10-15’), TO_DATE(‘2003-01-14’))`

    This example returns `-9` for the months between the two dates.

4.  `MONTHS_BETWEEN(TO_DATE(‘2003-10-13’), TO_DATE(‘2003-01-14’))`

    This example returns `-8` for the months between the two dates.


