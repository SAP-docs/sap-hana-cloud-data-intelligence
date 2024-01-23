<!-- loio45b5d1d8fdd34e009e4efc4a26b97bff -->

# Process Handlers

You can use the handler types to have more control over the behavior of the operators.

The following are the handler types that you can use.



<a name="loio45b5d1d8fdd34e009e4efc4a26b97bff__section_mhn_hcr_zcb"/>

## Initialization Handler

The initialization handler is set for an operator when it is created \(`v2_operator_create`\) and is invoked for every process that is instantiated for that operator.

The role of this handler is to initialize per-process data, resources, and connections, as required. Typically, the configuration values are also queried here.



<a name="loio45b5d1d8fdd34e009e4efc4a26b97bff__section_ers_hcr_zcb"/>

## Shutdown Handlers

In some cases, you use the `init` handler to only set a port handler. But, if it was a more complex case, you may have acquired some resources or allocated memory for that process individually. The place to clean up such resources is the shutdown handler:

```
// shutdown handler
const char* proc_shutdown( v2_process_t proc )
{
  // free proc's memory and resources here
}

// init handler
const char* proc_init( v2_process_t proc )
{
  ...
  v2_process_set_shutdown_handler( proc, proc_shutdown );
  ...
}
```

Shutdown handlers are called when the graph stops if \(and only if\) the `init` handler for that process was called \(regardless of its returned status\). This means that, the only case in which the shutdown handler will not be called is when the `init` handler is not even called because a previous process failed to initialize.



<a name="loio45b5d1d8fdd34e009e4efc4a26b97bff__section_l5j_wbr_zcb"/>

## Input Handlers

Operator input is given to the handler bound to the port that received the data. Port handlers are set per process instead of per operator. The handlers allow you to change the behavior of a process depending on its configuration properties. This means that, your operator can have different "modes" without having to check which one was set at every input.

An input port will be blocked while its handler is still running on the last piece of data it received. Therefore, the handler of a given port will never be called multiple times simultaneously, but rather sequentially for every consecutive piece of data. On the other hand, handlers for different ports may be called simultaneously depending on when each port received the input.

One port may not have multiple handlers. Calling `v2_process_set_port_handler` on an already bound port will replace the existing handler. This call can be useful to change the behavior of the process at runtime.



<a name="loio45b5d1d8fdd34e009e4efc4a26b97bff__section_z13_xbr_zcb"/>

## Timers

Timed handlers are a way of executing logic repeatedly without having to wait for the input on a port. They are completely independent from input ports and may, if desired, produce output. Use `v2_process_add_timed_handler` to register a timer.

Timed handlers are the only ones that may be registered multiple times, as they behave independently from one another, calling the provided callback function at every period.

For example, you can use a timer in an operator whose purpose is to generate random numbers at a specific interval:

```
// Timed handler
const char* gen_tick( v2_process_t proc )
{
  v2_datum_t datum = v2_datum_from_int64( rand() );
  v2_process_output( proc, "output", datum );
  v2_datum_release( datum );
  return NULL;
}

// Init handler
const char* gen_init( v2_process_t proc )
{
  ...
  v2_process_add_timed_handler(
    proc,
    "gen",     // Name to be used in the logs to tell handlers apart
    gen_tick,  // Handler function
    0,         // Repeat count (zero for unlimited)
    1000       // Interval (ms)
  );
  ...
}
```

