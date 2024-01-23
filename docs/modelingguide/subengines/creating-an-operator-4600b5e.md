<!-- loio4600b5ee3e2f43748ff250ae5a5da032 -->

# Creating an Operator

To register an operator, call `v2_operator_create` from `init` :

```
extern "C" V2_EXPORT void init( v2_context_t ctx )
{
  v2_operator_t op = v2_operator_create(
    ctx,             // the context passed by the engine to init
    "demo.strlen",   // operator ID; must be globally unique
    "Strlen Demo",   // user-friendly operator name
    init_strlen      // initialization handler (see below)
  );

  // Add an input port so the operator can receive and process data:
  v2_operator_add_input(
    op,         // pointer returned by v2_operator_create
    "inString", // port name; must be unique within this operator
    "string"    // port type
  );

  // Add an output port so the operator can send data:
  v2_operator_add_output( op, "outLength", "int64" );
}
```

The subengine does not impose any special format for port names, but we recommended prefixing them with `in` or `out`. The prefixing makes it easier to identify them apart when their names appear in the logs.

> ### Note:  
> We recommend that you namespace your operator IDs with a meaningful and unique prefix to avoid name clashes. For example, you can prefix with the operator IDs with the organization name.

`op` has an input port of type string and an output port of type `int64` . Now, define its initialization handler \(`init_strlen`\) that will be called every time a process is created to instantiate the `"demo.strlen"` operator:

```
const char* init_strlen( v2_process_t proc )
{
  v2_process_set_port_handler(
    proc,             // the process, created by the engine
    "inString",       // which port this handler is associated with
    strlen_on_input   // the actual handler (below)
  );

  return NULL; // no error
}

const char* strlen_on_input( v2_process_t proc, v2_datum_t datum )
{
  // Extract the string contained in `datum`
  const char* str = v2_datum_get_string( datum );

  size_t len = strlen( str );

  // Create the output datum containing the length
  // of the input string
  v2_datum_t out = v2_datum_from_int64( (int64_t)len );
  // Write it to the output port
  v2_process_output( proc, "outLength", out );
  // Release the `out` handle (see explanation below)
  v2_datum_release( out );

  return NULL; // no error
}
```

**Result**

You have created a basic operator. The initialization and termination, configuration properties, and timed handlers \(timers\) are described in the subsequent chapters of this guide.



<a name="loio4600b5ee3e2f43748ff250ae5a5da032__section_dnw_nd5_2db"/>

## Compiling an Operator Library

Compile the code to create an operator into a dynamic library \(shared object\), so that it can be consumed by the C++ subengine executable.

The minimal commands to compile are:

```
# Compile C/C++ sources into position-independent object files (.o)
$ gcc -c -fPIC <sources>
# Link the object files together into a shared object
$ gcc -shared -o <output-name>.so <object-files>
```

After compiling, you can place the `<output-name>.so` file in the `lib/` directory of the subengine and call `run.sh -j`. This call helps generate the JSON descriptions for your new operator.



<a name="loio4600b5ee3e2f43748ff250ae5a5da032__section_c5x_cf5_2db"/>

## Standard and External Libraries

The C++ subengine runs in a Docker container with Debian 9.2. This operating system provides `libstdc++.so.6` that the C++ subengine executable requires to consume the operators.

If your dynamic libraries use a different version or vendor, then you must either:

-   Compile with `-static-libstdc++`; or
-   Write a custom Dockerfile based on Debian 9.2 in which your desired Standard Library version or vendor is installed and available.

    > ### Caution:  
    > Do not replace `libstdc++.so.6` provided by the operating system.

    Next, associate your operator with the docker image by adding a tag using the `v2_operator_add_tag` function in your operator library.


The same concept applies to all external libraries on which the operators may depend. You can either link to them statically or include them in a custom Dockerfile.

