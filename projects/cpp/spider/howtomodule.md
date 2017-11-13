### spider/howtomodule

This page briefly explains the basics of `LogModule` development.

##### What is a LogModule ?
In terms of code, a `LogModule` is basically a class conforming to the `LogModule` interface.
In order to allow loading modules from dynamic libraries, we use C++ runtime polymorphism.
That means we have a `LogModule` class, from which all modules must inherit.

Dynamic libraries providing a module must also expose a `create` function with the following prototype:

```cpp
LogModule *create();
```
That function will be invoked everytime a new instance of the module is needed. The resulting pointer should be safe to `delete`.

##### The LogModule interface
The `LogModule` interface provides a generic interface for every log module.

```cpp
class LogModule : utils::NonCopyable
{
public:
    virtual ~LogModule() noexcept = default;

    virtual void appendEntry(const ILoggable &l) = 0;

    /** Flush potentially buffered data */
    virtual void flush() = 0;

    virtual void setRoot(const std::string &root) noexcept = 0;
    virtual void setID(const std::string &id) noexcept = 0;
    virtual void setIOManager(net::IOManager &mgr) noexcept = 0;

    /** Setup the handle. After this call, it must be ready to receive entries */
    virtual bool setup() noexcept = 0;
};
```

After loading a module, the 3 setters shall be called by the main program with the appropriate data.
After that, the `setup` method will be called. It should return `true` to indicate module readiness, or `false` otherwise.

When the module is active, its core functionality is the `appendEntry` method, which is used, as its names states, to add a new entry to the log.
The `flush` method can be called to ensure that any data buffered by the module is written and discarded.

##### Example: Implementing a printing module
To quickly sum up this page, we will now show the implementation of a basic module using the `LogModule` interface.
This module will be very simple, and will only output the data it is given to `stdout`.

```cpp
class PrintingLogModule : public LogModule
{
public:
  ~PrintingLogModule() noexcept override = default;

  void setRoot(const std::string &root) noexcept override
  {
    //This logger doesn't need a root
  }

  void setID(const std::string &id) noexcept override
  {
    _id = name;
  }

  void setIOManager(net::IOManager &manager) noexcept override
  {
    //This logger doesn't need an IOManager
  }

  bool setup() noexcept override
  {
    return true;
  }

  void appendEntry(const ILoggable &loggable) noexcept override
  {
    //We print the entry's stringified form
    std::cout << "[" << id << "]" << loggable.stringify() << std::endl;;
  }

  void flush() noexcept override
  {
    std::cout << std::flush;
  }

  static LogModule *create() noexcept
  {
    return new PrintingLogModule();
  }

private:
  std::string _id;
};

```