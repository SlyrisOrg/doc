### spider

The **Spider** is a client/server keylogger developed in C++.
It is cross-platform and has been tested on Linux, OSX and Windows.

##### The client
The client runs on an infected computer, and is responsible for recording events on it. Note that clients might have different features depending on the platform (see the [detailed feature list][0]).

[0]: http://doc.slyris.eu/projects/cpp/spider/features.html

It detects keystrokes, mouse movements and clicks events using the current platform API, and converts them to a universal format.
It can then log them locally or, if possible, send them to a remote server.

Clients should also open a secondary TCP channel and expect server-issued commands on it, so they can be remote-controlled.

##### The server
The server can run on any machine that can be discovered by its clients. Thus it can be network-local, or completely remote.
The server is responsible for accepting connections from clients in order to log the events they send. It can also connect itself on the clients' secondary channels and send commands through it.
The server associates a unique identifier to each client and records all events on disk. It uses rotating log files in order to keep them from becoming too big.

The server itself can be remote-controlled through a TCP connection: using a client ID, one can ask the server to send commands to a given client.

##### Client/Server communication
The client and the server communicate through TCP, using our own [protocol][1].
All messages are also secured using SSL.

[1]: http://doc.slyris.eu/projects/cpp/spider/protocol.html

##### User documentation
Detailed explanations and how-to's about using the project can be found [here][2].

[2]: http://doc.slyris.eu/projects/cpp/spider/userdoc.html

##### Developer documentation
Developer documentation (which contains implementation details and diagrams) is available [here][3].

[3]: http://doc.slyris.eu/projects/cpp/spider/devdoc.html
