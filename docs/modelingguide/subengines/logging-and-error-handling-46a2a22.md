<!-- loio46a2a225deef464d8f11cd8579d28d6b -->

# Logging and Error Handling

The C++ subengine defines the following logging levels:

-   `INFO` 
-   `DEBUG` 
-   `WARNING` 
-   `ERROR` 
-   `FATAL` 

The engine is in the debug mode when the debug tracing is enabled for the main engine. The debug messages are printed only when the engine is in the debug mode.

> ### Remember:  
> Fatal messages stop the graph execution. Error messages do not cause the graph execution to stop.

To log a single string, use the `v2_log_<level>_string` set of function that are declared in `v2/subengine.h`.

For convenience, the variadic functions \(such as, printf-like\) are declared and implemented in the optional `v2/log.h` header. If you want to include their implementation in your operator library, then before including `v2/log.h` in a source file, define the `V2_LOG_IMPLEMENTATION` macro.

> ### Tip:  
> Include in only one of your source files to avoid multiple definitions of those symbols.

For example:

```
#define V2_LOG_IMPLEMENTATION
#include <v2/log.h>
#undef V2_LOG_IMPLEMENTATION
```

This helps to include the header from multiple files at wherever those function declarations are required, and still continue to keep their implementation in a single place.



<a name="loio46a2a225deef464d8f11cd8579d28d6b__section_jd3_r35_2db"/>

## Error Handling

All types of handlers, which users can provide to the subengine have the return type, `const char*`. This return type is a null-terminated string containing the error message or a `NULL` value, if no error occurred. Errors returned by handlers are always fatal \(otherwise, use `v2_log_error_string` or `v2_log_error` instead\).

