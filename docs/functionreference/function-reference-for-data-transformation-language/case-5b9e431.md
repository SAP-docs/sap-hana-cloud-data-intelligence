<!-- loio5b9e4318c1fd46118700cbca8845743d -->

# CASE

CASE function allows the use of IF - THEN - ELSE logic.



<a name="loio5b9e4318c1fd46118700cbca8845743d__section_nn1_tzn_w4b"/>

## Syntax

`CASE [value] WHEN expression THEN expression [{WHEN expression THEN expression}…] [ELSE expression] END` 



<a name="loio5b9e4318c1fd46118700cbca8845743d__section_gtv_tzn_w4b"/>

## Description

A case expression allows the use of IF - THEN - ELSE logic. If the expression following the CASE statement \( `value` \) is equal to the expression following the WHEN statement, or if the expression following the WHEN statements evaluates to true and `value` is omitted, then the expression following the THEN statement is returned. Otherwise, the expression following the ELSE statement is returned if it exists.



<a name="loio5b9e4318c1fd46118700cbca8845743d__section_ump_wzn_w4b"/>

## Example

1.  `CASE “Status” WHEN 0 THEN ‘Pending’ ELSE ‘Done’ END`

    This example returns the value `Pending` if column `“Status”` has `0`, otherwise it returns `Done`.

2.  `CASE WHEN “Status” = 0 THEN ‘Pending’ ELSE ‘Done’ END`

    This example produces the same output as the previous one.


