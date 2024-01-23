<!-- loiocbc3749e9dee46b9be619bcf39361d02 -->

# TO\_DATE

TO\_DATE function converts a date string `d` into a DATE data type.



<a name="loiocbc3749e9dee46b9be619bcf39361d02__section_b5t_nrn_w4b"/>

## Syntax

`TO_DATE(d [, format])` 



<a name="loiocbc3749e9dee46b9be619bcf39361d02__section_c5t_nrn_w4b"/>

## Description

Converts a date string `d` into a DATE data type. The `format` must follow the Java SimpleDateFormat standard. If the `format` specifier is omitted, then the conversion is performed using the format `yyyy-MM-dd`.



<a name="loiocbc3749e9dee46b9be619bcf39361d02__section_rhb_qrn_w4b"/>

## Example

`TO_DATE(‘2010-01-12’, ‘yyyy-MM-dd’)`

This example converts the string `2010-01-12` to a DATE value using the format `yyyy-MM-dd`.

