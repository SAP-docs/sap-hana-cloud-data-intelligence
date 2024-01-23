<!-- loiodea7075047344ebbbf2bb5639f046a30 -->

# log.h

Declares and implements convenience wrappers for logging.

In one of your source files, add

> ### Source Code:  
> ```
> #define V2_LOG_IMPLEMENTATION
> #include "v2/log.h"
> #undef V2_LOG_IMPLEMENTATION
> ```

> ### Remember:  
> Always add the code block in only one of your source files.

This helps to compile the code with not only their declarations, but with also the definition of these functions. Everywhere else in your code, when `log.h` is included without the macro, it brings over the declarations only.

We recommend adding the code in only one of your source file, because it includes variadic functions that cannot be implemented within the engine for consumption from another binary. If you add them in more than one file, the executable would make assumptions about the implementation \(for plugin\) of variadic arguments that may not hold for different compiler vendors and versions.

> ### Tip:  
> If you do not prefer to use the convenience functions, and if you want to call only the `_string`-suffixed ones declared in the `subengine.h` header file, then it is not required to define the `V2_LOG_IMPLEMENTATION` macro or to include `log.h`.



<a name="loiodea7075047344ebbbf2bb5639f046a30__section_xvw_spg_fdb"/>

## Formatted Logging

The following are convenience functions to send `sprintf`-formatted strings to the engine log.

-   `void v2_log_info (const char *fmt,...)`
-   `void v2_log_debug (const char *fmt,...)`
-   `void v2_log_warning (const char *fmt,...)`
-   `void v2_log_error (const char *fmt,...)`
-   `void v2_log_fatal (const char *fmt,...)`

