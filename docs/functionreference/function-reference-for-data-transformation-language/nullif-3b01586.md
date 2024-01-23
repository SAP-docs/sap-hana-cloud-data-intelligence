<!-- loio3b015860c9ae4022832e7eb3332562fc -->

# NULLIF

NULLIF function compares the values of two input expressions.



<a name="loio3b015860c9ae4022832e7eb3332562fc__section_acs_gc4_w4b"/>

## Syntax

`NULLIF(expression1, expression2)` 



<a name="loio3b015860c9ae4022832e7eb3332562fc__section_bcs_gc4_w4b"/>

## Description

NULLIF compares the values of two input expressions. If the first expression equals the second expression, NULLIF returns NULL.

-   If `expression1` does not equal `expression2` , NULLIF returns `expression1` .
-   If `expression2` is NULL, NULLIF returns `expression1`.



<a name="loio3b015860c9ae4022832e7eb3332562fc__section_ff3_nc4_w4b"/>

## Example

1.  `NULLIF(‘diff’, ‘same’)`

    This example returns `diff`.

2.  `NULLIF(‘same’, ‘same’)`

    This example returns `NULL`.


