<!-- loiof2a5fb149b9e4524ac06d2086fb98bae -->

# Getting Started with the C++ Subengine

At initialization, the C++ subengine iterates recursively over the contents of its `lib/` directory \(in the root folder of the subengine\) and loads each shared object \(`.so`\) file.

Use the recursive iteration to organize your libraries into subdirectories, as necessary. The subengine processes only shared object \(`.so`\) files and ignores other file types.

The C++ subengine also expects to find a symbol called `init` in each of the shared objects. This function in pure C is a function with signature as follows:

```
V2_EXPORT void init( v2_context_t ctx ) { ... }
```

> ### Note:  
> If you compile your library from C++, you must prepend the function declaration with `extern "C"` to prevent name mangling.

The signatures of the `init` function use the `V2_EXPORT` macro to ensure that the symbol is visible from the engine executable. The main role of the `init` function is to tell the C++ subengine about the operators implemented by this library. Therefore, before its subgraph is received, the application calls the `init` function once when the engine starts running.

