<!-- loio4c4d340a802c4aa888f801abbdd48225 -->

# COALESCE

COALESCE function returns the first non-NULL expression from a list.



<a name="loio4c4d340a802c4aa888f801abbdd48225__section_tj4_d14_w4b"/>

## Syntax

`COALESCE(expression_list)`



<a name="loio4c4d340a802c4aa888f801abbdd48225__section_uj4_d14_w4b"/>

## Description

Returns the first non-NULL expression from a list. At least two expressions must be contained in `expression_list`, and all expressions must be comparable. The result will be NULL if all the arguments are NULL.



<a name="loio4c4d340a802c4aa888f801abbdd48225__section_ish_f14_w4b"/>

## Example

`COALESCE(NULL, 10)`

This example returns the value `10`.

