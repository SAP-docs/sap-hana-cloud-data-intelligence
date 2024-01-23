<!-- loio98c3740a961d457a9fb8387e9e8e6157 -->

# TO\_INTEGER

TO\_INTEGER function converts the value to an INTEGER data type with the specified length.



<a name="loio98c3740a961d457a9fb8387e9e8e6157__section_mz3_htn_w4b"/>

## Syntax

`TO_INTEGER(value [, length])` 



<a name="loio98c3740a961d457a9fb8387e9e8e6157__section_nz3_htn_w4b"/>

## Description

Converts the value to an INTEGER data type with the specified length. The `length` is expressed as number of bytes ans the possible values are 1, 2, 4 \(default\) and 8. If the input value has a mantissa, these digits are truncated during the conversion process.



<a name="loio98c3740a961d457a9fb8387e9e8e6157__section_s2m_jtn_w4b"/>

## Example

1.  `TO_INTEGER(‘10’)`

    This example converts the value `10` to an integer value `10`

2.  `TO_INTEGER(10.5)`

    This example converts the value `10.5` to an integer value `10`, truncating the mantissa.


