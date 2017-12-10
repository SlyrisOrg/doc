### core/lib

**lib** is a module dedicated to shared library loading.

##### What does it do ?
It allows importing and using symbols from shared libraries into the main program.
For example, it can be used to create things such as a plugin system.

It is compatible with C and C++, provided that the loaded symbol names are not mangled.

It has been tested on Linux, OSX and Windows, and should seamlessly support other POSIX-compliant operating systems.

##### Example
The example below illustrates the loading of the function `double_this` from a C library called `lol` into a C++ program.

```c
#ifdef WIN32
#define EXPORT_SYMBOL __declspec(dllexport)
#else
#define EXPORT_SYMBOL
#endif

EXPORT_SYMBOL int double_this(int number)
{
    return number * 2;
}
```

```cpp
lib::SharedLibrary lib;

//The library should be called liblol.so on Linux, or lol.dll on Windows,
//but the implementation can "guess" its full name.
lib.load(fs::path("lol"), lib::LoadingMode::Default);

if (lib.isLoaded()) {
	auto double_this = lib.get<int(int)>("double_this");
	int result = double_this(2); //result is now 4;
}
```