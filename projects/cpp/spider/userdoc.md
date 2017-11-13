### spider/user

This page provides all the knowledge required to build the project and use it.

##### Building
In order to build the project from the sources, CMake (>= 3.8), Boost system libraries, and a compiler supporting C++17 (or MSVC) are required.

The sources are separated into two repositories because both parts of the software are usually not used on the same machine.

Assuming we are in either project's directory, the following commands can be used to build it:
```bash
user@host> mkdir build
user@host> cd build
user@host> cmake -DCMAKE_BUILD_TYPE=Release ..
user@host> make
```

*Note that the default `make` invocation also builds unit tests.*

Binaries are generated in the project's root in a `bin` directory.


##### Using the server
The server can be launched as-is without any parameter, or can also be configured at runtime through command line options.

```bash
user@host> ./spider_server --help
```
```
Available options:
  --port arg (=31337)          the port at which to listen
  --log_dir arg (=spider_logs) the directory in which to store log data
  --cmd_port arg (=31338)      port on which to allow shell connection
  --cert arg (=cert.pem)       the certificate to use for SSL connections
  --key arg (=key.pem)         the private key to use for SSL connections
  --help                       display this help message
```

##### Using the client
The server can be launched as-is without any parameter, however in most cases, the address and port at which the server can be reached need to be configured.

Just like the server, this (and more) can be tweaked from the command line.

```bash
user@host> ./spider_client --help
```
```
Available options:
  --port arg (=31337)           the port on which to connect
  --port-acceptor arg (=31300)  the port at which to listen
  --address arg (=79.137.42.80) the address of the server to connect to
  --log-dir arg (=NotAVirus)    the directory in which to store log data
  --cert-file arg (=cert.pem)   the certificate to use for SSL connections
  --key-file arg (=key.pem)     the private key to use for SSL connections
  --retry-time arg (=20)        the frequency at which connections should be attempted
  --help                        display this help message
```

*Note that on Linux and OSX, the client has to be run with super-user privileges*

##### Log modules
Both the client and the server perform logging tasks.
The behavior of these tasks can be customised through plugins called **log modules**.
Each module is responsible for handling loggable data on its own when called by the main program.

|          Name         |                           Description                           |
|-----------------------|-----------------------------------------------------------------|
| RotatingFileLogModule | Logs data in human-readable files, rotating to avoid huge files |
|   JSONFileLogModule   | Logs data in JSON-based files, rotating to avoid huge files     |
| APIConnectedLogModule | Forwards data to a REST API by sending it as JSON data          |
|  ForwardingLogModule  | Forwards data to another host using the Spider protocol         |


##### Runtime logging
By default, all our programs emit debugging information through loggers. This behavior can be configured through the command line using the environment.

Each logger can be identified with a name, which is given to it at initialization.
Each logging message is associated with a logger and a severity level.
It is then possible to specify a minimum level for a logger by defining the environment variable `LOGGER_CONFIG` like shown below:

```bash
user@host> export LOGGER_CONFIG="alogger:warning,anotherlogger:error"
```

With the above, `alogger` would only report warnings and errors, meanwhile `anotherlogger` would only report errors.


All logging output can also be permanently disabled at compile-time by defining the `LOGGER_DISABLE_ALL` macro.

