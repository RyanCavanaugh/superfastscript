# Superfastscript

Superfastscript is a typesafe WebAssembly-ready variant of JavaScript. Superfastscript programs can be directly compiled to WASM, but use a syntax very similar to JavaScript.

# Motivation

Typed languages like TypeScript are well-suited to normal JS development, but the current WebAssembly Minimal Viable Product doesn't support many features of JavaScript people have come to know and love.
Superfastscript imposes certain limitations on existing JavaScript, and adds some new syntax variants, to allow JS programmers to quickly write WASM-ready programs.

# Intentional Limitations

We need a *subset* of typed JavaScript that excludes certain features unsupported by WASM:
* The JS standard library
* JS objects
* Closures
* Exceptions / `try`/`catch`/`finally`

# New Features

Superfastscript adds some new language features that are missing in JavaScript.

### Manual Memory Management

Because WASM lacks a garbage collector, we're also going to want some new primitives
 * `malloc` - the *manually allocate* function allocates memory
 * `free` - the *finite resource eraser extension* function undoes `malloc`

### Pointers

Superfastscript adds pointers, a long-missing feature of JavaScript.
Pointers can point to primitives *or* arbitrary buffers without loss of generality.

# Introductory Tutorial

### A minimal Superfastscript program

Superfastscript changes the function syntax slightly. We omit the `function` keyword and write the return type instead:
```c
int main()
{
    return 0;
}
```

### Variables

You can declare variables with familiar `var x;` syntax. Except instead of `var`, we'll write the type name:
```c
int main()
{
    int x = 100;
    return x;
}
```

### Pointers and Memory

You can use the *manual allocate* function, `malloc`, to allocate blocks memory:
```c
int* ptr = malloc(sizeof(int) * 24);
```

These pointers are similar to other brace-using languages. For example, you can modify an array (really just a pointer) element:
```c
// Increment the 15th element of the manually-allocated array
ptr[14]++;
```

Once a memory block is allocated, use the *finite resource eraser extension* function, `free`, to release it:
```c
free(ptr);
```

# Documentation

Additional reading is available:
 * [The Superfastscript programming language](https://en.wikipedia.org/wiki/The_C_Programming_Language)
 * [Wikibooks: Superfastscript programming](https://en.wikibooks.org/wiki/C_Programming)

