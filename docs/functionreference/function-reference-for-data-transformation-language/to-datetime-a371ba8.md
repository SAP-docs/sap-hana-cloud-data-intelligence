<!-- loioa371ba8c628d487aa5eedab387708d15 -->

# TO\_DATETIME

TO\_DATETIME function converts a date string `d` into the DATETIME data type



<a name="loioa371ba8c628d487aa5eedab387708d15__section_igt_2sn_w4b"/>

## Syntax

`TO_DATETIME(d [, format])` 



<a name="loioa371ba8c628d487aa5eedab387708d15__section_jgt_2sn_w4b"/>

## Description

Converts a date string `d` into the DATETIME data type. The `format` must follow the Java SimpleDateFormat standard. If the `format` specifier is omitted, then the conversion is performed using the format `yyyy-MM-dd HH:mm:ss.SSS`.



<a name="loioa371ba8c628d487aa5eedab387708d15__section_q1p_gsn_w4b"/>

## Example

`TO_DATETIME(‘2010-01-11 13:30:00’, ‘yyyy-MM-dd HH:mm:ss’)`

This example converts the string `2010-01-11 13:30:00` to a DATETIME value using the format `yyyy-MM-dd HH:mm:ss`.

