<!-- loioc1886577da8a4f52a742715d8e886793 -->

# TO\_DECIMAL

TO\_DECIMAL function converts a value to a DECIMAL data type.



<a name="loioc1886577da8a4f52a742715d8e886793__section_ewz_msn_w4b"/>

## Syntax

`TO_DECIMAL(value [, precision, scale])`



<a name="loioc1886577da8a4f52a742715d8e886793__section_fwz_msn_w4b"/>

## Description

Converts a value to a DECIMAL data type. The `precision` is the total number of significant digits and can range from 1 to 34. The scale is the number of digits from the decimal point to the least significant digit and can range from -6,111 to 6,176. This means that the scale specifies the range of the exponent in the decimal number from `10e-6111` to `10e6176` . If the scale is not specified, it defaults to 0. Scale is positive when the number has significant digits to the right of the decimal point, and negative when the number has significant digits to the left of the decimal point.

When precision and scale are not specified, DECIMAL becomes a floating-point decimal number. In this case, precision and scale can vary within the range described above, 1~34 for precision and -6,111~6,176 for scale depending on the stored value. Unrequired least significant digits in the mantissa of the input value are truncated during the conversion process.



<a name="loioc1886577da8a4f52a742715d8e886793__section_p3f_rsn_w4b"/>

## Example

`TO_DECIMAL(7654321.888888, 10, 3)`

This example converts the value `7654321.888888` to a DECIMAL data type with `10` digits precision and a scale of `3`, and returns the value `7654321.888`.

