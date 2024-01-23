<!-- loio3cfd283a222043e899dbdd57f7e25073 -->

# QUARTER

QUARTER function \(Date & Time\) returns the numerical year quarter of date `d`.



<a name="loio3cfd283a222043e899dbdd57f7e25073__section_ynx_msh_bpb"/>

## Syntax

`QUARTER(d [, start_month ])`



<a name="loio3cfd283a222043e899dbdd57f7e25073__section_znx_msh_bpb"/>

## Description

Returns the numerical year quarter of date `d`. The first quarter starts in the month specified by `start_month`. If `start_month` is not specified the first quarter is assumed to begin in January.



<a name="loio3cfd283a222043e899dbdd57f7e25073__section_byp_psh_bpb"/>

## Example

`QUARTER(TO_DATE(‘2012-01-01’, ‘yyyy-MM-dd’), 2)`

This example returns the value `2011-Q4` as the year and quarter for the specified date.

