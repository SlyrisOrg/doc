### core

**core** is our base library for most C++ projects.

##### Modules
The library is divided into modules of varying sizes, each of which has a precise purpose.

At the moment, **core** contains the following modules:

|     Module name     |        Module description        |
|---------------------|----------------------------------|
| [config][0]         | Compiler/Platform detection      |
| [lib][1]            | Shared library management        |
| [log][2]            | Conditionnal logging             |
| [meta][3]           | Basic metaprogramming utilities  |
| [net][4]            | Network utilities                |
| [opt][5]            | Basic option parser              |
| [pp][6]             | Preprocessing utilities          |
| [utils][7]          | Lots of tiny utilities           |

[0]: http://doc.slyris.eu/projects/cpp/core/config.html
[1]: http://doc.slyris.eu/projects/cpp/core/lib.html
[2]: http://doc.slyris.eu/projects/cpp/core/log.html
[3]: http://doc.slyris.eu/projects/cpp/core/meta.html
[4]: http://doc.slyris.eu/projects/cpp/core/net.html
[5]: http://doc.slyris.eu/projects/cpp/core/opt.html
[6]: http://doc.slyris.eu/projects/cpp/core/pp.html
[7]: http://doc.slyris.eu/projects/cpp/core/utils.html

Each module is documented on its own page, accessible through the links in the table above.

##### Using the library
Traditionnally, we add the **core** repository as a submodule in every C++ project.

##### Importing a module
From a CMake point-of-view, a module is a library, so to import a module of **core** into an external project, we just have to link on the corresponding library.
**CMake** will automatically add sources dependencies and appropriate include directories.

Here is an example, assuming the executable name is `my_project`:
```cmake
# We add the "meta" module as a dependency of the "my_project" target
target_link_libraries(my_project PUBLIC core-meta)
```

##### Creating a new module
To create a module in **core**, we first need to create a subdirectory for it, and add it to the top-level `CMakeLists.txt`.
The subdirectory will contain a `CMakeSources.cmake` file listing the sources of the module, and a `CMakeLists.txt` file.

Here is an example for the latter:

```cmake
# We include the CMakeSources.cmake file
include(CMakeSources.cmake)

# We add a library with the INTERFACE keyword in order to specify it as header-only
add_library(core-meta INTERFACE)

# We add the sources of the library
target_sources(core-meta INTERFACE ${META_PUBLIC_HEADERS})

# We add the include_directories of our interface library and specify its install directory
target_include_directories(core-meta INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:${CMAKE_SOURCE_DIR}/Core-CPP/meta>)
```
