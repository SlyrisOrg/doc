### spider/dev

This page explains in detail the architecture of both sides of the Spider project. It assumes the reader already has basic knowledge of [the protocol][0].

[0]: http://doc.slyris.eu/projects/cpp/spider/protocol.html

##### Handling events
Both Spider binaries are said to be event-driven. That means the event-handling mechanisms are at the very core of the project.
Events are handled with a classic event-loop, in which events can be watched and associated with callbacks.

In the Spider, the class responsible for managing that event-loop is the `IOManager`.
Other classes, such as network-related ones or simply timers, can be attached to an instance of the `IOManager` class when constructed.

The example below shows how a timer can be registered and waited upon:

```cpp
IOManager mgr;
Timer fiveSecTimer(mgr, 5);

fiveSecTimer.asyncWait(std::bind([](const ErrorCode &err) {
    std::cout << "This will be printed in 5 seconds" << std::endl;
}, net::ErrorPlaceholder));

mgr.run();
```

##### Managing data
The most important task of the Spider is to manage the data it receives.
A typical example of data handling is to store everything into log files.
However, in order to allow tweaking that behavior, the Spider provides a plugin system based on the `LogModule` interface.

This interface defines a `LogModule` as an object to which we can send entries (an entry being a piece of data to be handled).
Here is [how to implement a module][1].

[1]: http://doc.slyris.eu/projects/cpp/spider/howtomodule.html

##### Client: watching user input
In order to watch user input, the Spider client has a `KeyLogger` class.
That class is responsible for monitoring input events, and accepts user-defined callbacks, which will be called for each appropriate event.

The implementation of the `KeyLogger` class depends on the platform.

##### Client: Viral behavior
As any malware, the client must implement a viral behavior of some sort.
In our implementation, this goes through the `Viral` class.
This class provides, among other features, anti-tracing and arbitrary shell execution.

Of course, the underlying implementation of that class depends on the platform.

Here is detailed documentation about [how to implement a keylogger][2].

[2]:http://doc.slyris.eu/projects/cpp/spider/howtokeylog.html