<!-- loio1e58b273857d46dd8f7a2912accae34c -->

# DAYS\_BETWEEN

DAYS\_BETWEEN function \(Date & Time\) computes the number of days between `d1` and `d2`.



<a name="loio1e58b273857d46dd8f7a2912accae34c__section_jpp_p4h_bpb"/>

## Syntax

`DAYS_BETWEEN(d1, d2)`



<a name="loio1e58b273857d46dd8f7a2912accae34c__section_kpp_p4h_bpb"/>

## Description

Computes the number of days between `d1` and `d2`.



<a name="loio1e58b273857d46dd8f7a2912accae34c__section_xdr_r4h_bpb"/>

## Example

1.  `DAYS_BETWEEN(TO_DATE(‘2009-12-05’, ‘yyyy-MM-dd’), TO_DATE(‘2010-01-05’, ‘yyyy-MM-dd’))`

    This example returns the value `31` for days between the two dates specified.

2.  `DAYS_BETWEEN(‘2018-02-07 23:00:00’, ‘2018-02-08 01:00:00’)`

    This example returns the value 0 for days between the two specified dates.

3.  `DAYS_BETWEEN(‘2018-02-07 23:00:00’, ‘2018-02-08 23:00:00’)`

    This example returns the value 1 for days between the two specified dates.


