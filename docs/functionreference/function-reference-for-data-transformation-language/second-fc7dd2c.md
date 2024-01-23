<!-- loiofc7dd2c3aca442e080d65e28be375cc4 -->

# SECOND

SECOND function \(Date & Time\) returns a value of the seconds for a given time.



<a name="loiofc7dd2c3aca442e080d65e28be375cc4__section_d14_xsh_bpb"/>

## Syntax

`SECOND(t)`



<a name="loiofc7dd2c3aca442e080d65e28be375cc4__section_e14_xsh_bpb"/>

## Description

Returns a value of the seconds for a given time. Subseconds are included for DATETIME datatypes.



<a name="loiofc7dd2c3aca442e080d65e28be375cc4__section_zgs_zsh_bpb"/>

## Example

1.  `SECOND(TO_TIME(‘12:34:56’))`

    This example returns the value `56` for the seconds of the specified time.

2.  `SECOND(‘2014-03-25 12:34:56.789’)`

    This example returns the value `56.789` for the subseconds of the specified time.


