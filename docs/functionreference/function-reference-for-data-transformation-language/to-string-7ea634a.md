<!-- loio7ea634abd7074d5d8bbe288244b8a672 -->

# TO\_STRING

TO\_STRING function converts a value to a STRING data type.



<a name="loio7ea634abd7074d5d8bbe288244b8a672__section_k1p_5tn_w4b"/>

## Syntax

`TO_STRING(value [, format])` 



<a name="loio7ea634abd7074d5d8bbe288244b8a672__section_l1p_5tn_w4b"/>

## Description

Converts a value to a STRING data type. If `value` is of data type DATE, TIME or DATETIME, the output `format` can be specified following the Java SimpleDateFormat standard. If the `format` specifier is omitted for a DATE, TIME, or DATETIME value, then the conversion is performed using the default format of the type: `yyyy-MM-dd` for DATE, `HH:mm:ss` for TIME, and `yyyy-MM-dd HH:mm:ss.SSS` for DATETIME.



<a name="loio7ea634abd7074d5d8bbe288244b8a672__section_vzj_xtn_w4b"/>

## Example

`TO_STRING(TO_DATE(‘2009-12-31’), ‘MM/dd/yy’)`

This example converts the DATE value `2009-12-31` to the STRING value `12/31/09`.

