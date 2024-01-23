<!-- loioba9ca25241714468810ea514a2d2ea1e -->

# ROUND

The ROUND function rounds a given value to the specified number of places after the decimal point.



<a name="loioba9ca25241714468810ea514a2d2ea1e__section_h3p_xzd_t4b"/>

## Syntax

<code>ROUND(<i class="varname">&lt;n&gt;</i> [, <i class="varname">&lt;pos&gt;</i>])</code> 



<a name="loioba9ca25241714468810ea514a2d2ea1e__section_i3p_xzd_t4b"/>

## Description

When given a value in <code><i class="varname">&lt;n&gt;</i></code> and a specified number of decimal points in <code><i class="varname">&lt;pos&gt;</i></code>, the ROUND function returns a value. By default, the ROUND function follows the half round method of rounding. That is, the value <code><i class="varname">&lt;n.n&gt;</i></code> is rounded up to the next round figure.

> ### Note:  
> When using ROUND with floating point types of numbers, the precision of the numeric representation can affect the obtained result. For floating point types, the actual number of digits after the decimal point is influenced by the precision of the type used.
> 
> > ### Example:  
> > The result of `ROUND(TO_FLOATING(399.71429443359375),2)` is 399.7099914550781 and not 399.71.



> ### Example:  
> -   The following function returns `16.2`: `ROUND(16.16, 1)`.
> -   The following function returns `20`: `ROUND(16.16, -1)`.
> -   The following function returns `1234.1000`: `ROUND(1234.1234, 1)`.

