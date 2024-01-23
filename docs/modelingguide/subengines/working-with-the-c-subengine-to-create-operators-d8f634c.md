<!-- loiod8f634ca17914f27953f28a757c04232 -->

# Working with the C++ Subengine to Create Operators

The SAP Data Intelligence Modeler C++ subengine lets you code your own operators in C++ and make them available for use from the Modeler application.



<a name="loiod8f634ca17914f27953f28a757c04232__section_z1k_cwt_2db"/>

## Introduction

> ### Note:  
> The C++ Subengine is deprecated. It will be removed in a future SAP Data Intelligence release.

The C++ subengine detects and runs operators that are compiled into shared objects \( `*.so` \). When you run a graph in the modeler application, the main engine \(which also serves the user interface over HTTP\) breaks the graph into large subgraphs. With large subgraphs, the same subengine runs every operator in a subgraph. The main engine then runs a subengine process for each subgraph.

When launched, the C++ subengine performs the following tasks:

1.  Looks for and registers operators.
2.  Initializes the mechanisms for communicating with the main engine.
3.  Receives its subgraph from the main engine.
4.  Instantiates the processes in the subgraph and initializes them.
5.  Sets up the connections among processes.
6.  Starts the graph, handles its input, invokes user-supplied handlers, and writes the output.
7.  When instructed by the main engine to stop, or when a fatal error occurs, it cleans up and terminates.



<a name="loiod8f634ca17914f27953f28a757c04232__section_epw_fwt_2db"/>

## Quick Start

```
#include <v2/subengine.h>

// Port handler
const char* echo_input( v2_process_t proc, v2_datum_t datum )
{
  // Write the input unchanged
  v2_process_output( proc, "output", datum );
  return NULL; // No error
}

// Shutdown handler (optional)
const char* echo_shutdown( v2_process_t proc )
{
  // Clean up echo's resources here.
  return NULL;
}

// Init handler
const char* echo_init( v2_process_t proc )
{
  // Call echo_input whenever port "input" receives data
  v2_process_set_port_handler( proc, "input", echo_input );
  // Call echo_shutdown when the process is stopped
  v2_process_set_shutdown_handler( proc, echo_shutdown );
  return NULL;
}

// Init function
// Remove `extern "C"` when compiling as pure C
extern "C" V2_EXPORT void init( v2_context_t ctx )
{
  // Create an operator called "Echo" with ID "demo.echo" and call
  // echo_init when initializing its processes.
  auto op = v2_operator_create( ctx, "demo.echo", "Echo", echo_init );
  // Add an input port called "input" of type string.
  v2_operator_add_input( op, "input", "string" );
  // Add an output port called "output" of type string.
  v2_operator_add_output( op, "output", "string" );
}
```

-   **[Getting Started with the C++ Subengine](getting-started-with-the-c-subengine-f2a5fb1.md "At initialization, the C++ subengine iterates recursively over the contents of its lib/ directory (in the root folder of
		the subengine) and loads each shared object (.so) file.")**  
At initialization, the C++ subengine iterates recursively over the contents of its `lib/` directory \(in the root folder of the subengine\) and loads each shared object \(`.so`\) file.
-   **[Creating an Operator](creating-an-operator-4600b5e.md "To register an operator, call v2_operator_create from
      init :")**  
To register an operator, call `v2_operator_create` from `init` :
-   **[Logging and Error Handling](logging-and-error-handling-46a2a22.md "The C++ subengine defines the following logging levels:")**  
The C++ subengine defines the following logging levels:
-   **[Port Data](port-data-28a448b.md "Port types are not known at compile time. The subengine uses the handle,
			v2_datum_t to carry the generic inputs and outputs between the
		operators. The v2_datum_t handle is a reference-counted handle to an
		underlying piece of data.")**  
Port types are not known at compile time. The subengine uses the handle, `v2_datum_t` to carry the generic inputs and outputs between the operators. The `v2_datum_t` handle is a reference-counted handle to an underlying piece of data.
-   **[Setting Values for Configuration Properties](setting-values-for-configuration-properties-ce22148.md "You set the configuration properties at the operator level and each property is
		associated with a default value.")**  
You set the configuration properties at the operator level and each property is associated with a default value.
-   **[Process Handlers](process-handlers-45b5d1d.md "You can use the handler types to have more control over the behavior of the
		operators.")**  
You can use the handler types to have more control over the behavior of the operators.
-   **[API Reference](api-reference-347c826.md "Use the C++ API to create operators and to work with the SAP Data Intelligence
		subengine.")**  
Use the C++ API to create operators and to work with the SAP Data Intelligence subengine.

