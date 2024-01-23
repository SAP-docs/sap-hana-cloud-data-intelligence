<!-- loio33cefca985144e5a883887e015ff71b0 -->

# Node.js Safe and Unsafe Integer Data Types

Because JavaScript doesn't have an integer data type, there are safe and unsafe integer data types when you use the Node.js subengine.

SAP Data Intelligence Modeler converts JavaScript number data type to uint64 or int64. The Modeler represents a number data type internally as an IEEE-754 double precision float. Therefore, for Node.js, SAP Data Intelligence Modeler represents only integer values up to 53 bits. Any integer value greater than 53 bits is an unsafe integer data type.

To prevent silent and undetected problems with the JavaScript number conversion, the Node.js subengine stops with a corresponding error message when it receives or sends an unsafe integer value. If a Node.js operator has an unsafe integer value, the corresponding graph also stops.

An unsafe integer value is defined as follows:

> ### Sample Code:  
> ```
> Number.isSafeInteger(data) === false
> ```

The safe integers consist of all integers from -\(253 — 1\) to 253 — 1 \(inclusive\). Therefore, the full range of SAP Data Intelligence Modeler types uint64 and int64 can't be represented in Node.js JavaScript.

```
type uint64 - range: 0 … 2**64 -1 (0 through 18446744073709551615)
type int64: -(2**63 -1) … 2**63 –1 (-9223372036854775808 through 9223372036854775807)
```

If converted into number, the mathematical rules of equality can be violated in JavaScript as shown in the following example code snippet:

```

( 1 === 2 ) === false // <- this always evaluates to false and is mathematically exact
    
// Now, add MAX_SAFE_INTEGER to both sides:
( 1 + Number.MAX_SAFE_INTEGER === 2 + Number.MAX_SAFE_INTEGER ) === true // <- results to true       
// Also a legal expression, it is mathematically incorrect 
```

For more information about safe integers, see the external link [developer.mozilla.org, datatype \(IEEE-754\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isSafeInteger).

