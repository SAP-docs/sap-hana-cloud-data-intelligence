<!-- loio11fa6039040344719e669cba855e562b -->

# IFNULL

IFNULL function returns the first not NULL input expression.



<a name="loio11fa6039040344719e669cba855e562b__section_vwt_514_w4b"/>

## Syntax

`IFNULL(expression1, expression2)` 



<a name="loio11fa6039040344719e669cba855e562b__section_wwt_514_w4b"/>

## Description

Returns the first not NULL input expression.

-   Returns `expression1` if `expression1` is not NULL.
-   Returns `expression2` if `expression1` is NULL.
-   Returns NULL if both input expressions are NULL.



<a name="loio11fa6039040344719e669cba855e562b__section_a4j_x14_w4b"/>

## Example

1.  `IFNULL(‘diff’, ‘same’)`

    This example returns `diff`

2.  `IFNULL(NULL, ‘same’)`

    This example returns `same`.

3.  `IFNULL(NULL, NULL)`

    This example returns `NULL`


