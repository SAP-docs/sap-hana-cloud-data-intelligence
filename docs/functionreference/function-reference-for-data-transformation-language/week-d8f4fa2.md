<!-- loiod8f4fa2abcbd44c8830fbe59d1832828 -->

# WEEK

WEEK function \(Date & Time\)



<a name="loiod8f4fa2abcbd44c8830fbe59d1832828__section_nf1_pth_bpb"/>

## Syntax

`WEEK(d)`



<a name="loiod8f4fa2abcbd44c8830fbe59d1832828__section_of1_pth_bpb"/>

## Description

Returns the week number of date `d`.



<a name="loiod8f4fa2abcbd44c8830fbe59d1832828__section_jry_pth_bpb"/>

## Example

1.  `WEEK(TO_DATE(‘2011-05-30’, ‘yyyy-MM-dd’))`

    This example returns the value `23` for the week number of the specified date.

2.  `WEEK(TO_DATE(‘2016-12-31’), ‘yyyy-MM-dd’)`

    This example returns the value `53` for the week number of the specified date.

3.  `WEEK(TO_DATE(‘2017-01-01’), ‘yyyy-MM-dd’)`

    This example returns the value `1` for the week number of the specified date.

4.  `WEEK(TO_DATE(‘2017-01-02’, ‘yyyy-MM-dd’))`

    This example returns the value `2` for the week number of the specified date.


