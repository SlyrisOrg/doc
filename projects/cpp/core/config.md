### core/config

**config** is a module providing platform-dependent or compiler-dependent features.

The compatible platforms are Linux, OSX and Windows.
The compatible compilers are GCC, CLang and MSVC.

##### USING_LINUX, USING_OSX, USING_WINDOWS
These macros are conditionnally defined for the appropriate platforms. They provide a standardized and easy way to identify the platform at compile-time.

```cpp
#if defined(USING_LINUX)
//Do Linux-specific stuff
#elif defined(USING_OSX)
//Do OSX-specific stuff
#elif defined(USING_WINDOWS)
//Do Windows-specific stuff
#else
#error unsupported platform
#endif
```

##### USING_GCC, USING_CLANG, USING_MSVC
These macros are conditionnally defined for the appropriate compilers. They provide a standardized and easy way to identify the compiler at compile-time.

```cpp
#if defined(USING_GCC)
//Do GCC-specific stuff
#elif defined(USING_CLANG)
//Do CLang-specific stuff
#elif defined(USING_MSVC)
//Do bad stuff
#else
#error unsupported compiler
#endif
```

##### always_inline
The `always_inline` attribute can be used to force inlining of a function.

```cpp
static always_inline uselessFunction() noexcept
{
}
```

##### likely, unlikely
The `likely`/`unlikely` functions allow providing branch prediction hints to the compiler.
They can be used for boolean expressions, and return the truth value they were given as parameter.

```cpp
if (unlikely(functionThatIsNeverSupposedToFail() == FAILURE)) {
}
```

##### EXPORT_SYMBOL
The `EXPORT_SYMBOL` macro allows changing the visibility of the symbol it marks, in order to make it visible outside the binary file.
This is mainly used to achieve dynamic symbol loading of objects from shared libraries.

```cpp
EXPORT_SYMBOL extern int a_number;
//a_number can now be seen by potential dynamic library loaders.
```