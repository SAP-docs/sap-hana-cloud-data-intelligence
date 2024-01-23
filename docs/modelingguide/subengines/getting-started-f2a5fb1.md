<!-- loiof2a5fb149b9e4524ac06d2086fb98bae -->

# Getting Started

At initialization, the subengine recursively iterates over the contents of its `lib/` directory \(in the root folder of the subengine\) and loads each `.so` file.

You can use the fact that the iteration is recursive to organize your libraries into subdirectories as necessary. The subengine ignores files that do not end in `.so`.

The engine also expects to find a symbol called `init` in each of those shared objects. In pure C, this must be a function with signature:

```
V2_EXPORT void init( v2_context_t ctx ) { ... }
```

> ### Note:  
> If you compile your library from C++, mandatorily prepend the function declaration with `extern "C"` to prevent name mangling.

The signatures of the `init` function use the `V2_EXPORT` macro to ensure that the symbol is visible from the engine executable.

The main role of the `init` function is to tell the engine about the operators implemented by this library. Thus, this function is called once when the engine starts running, before its subgraph is even received.

