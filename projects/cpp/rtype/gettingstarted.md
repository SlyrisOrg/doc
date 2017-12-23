### dev/start

##### Getting the code
The first thing to do is obviously getting the full code.
At the moment, it is hosted on Gerrit in the `rtype_client` and `rtype_server` repositories.

To update the code and the submodules to their latest versions, you can use the `pull.sh` script (or regular Git commands).

##### Compiling the code
The project has been developed and tested on the following platforms and compilers: Linux (GCC 7.2), OSX (CLang 5.0) and Windows (MSVC 15.6).
We used CMake 3.10 as a build system.

If you want to compile everything, including the unit tests, you can just run the `jenkins-build` script that matches your platform.
Otherwise, you can use CMake to target your preferred generator and then build only what you want.
All the binaries are created in the `bin` directory at the root of the repository, and should be launched from there.