### spider/howtokeylog

This page briefly explains the basics of `Keylogger` development.

##### What is a Keylogger ?
A keylogger is a unit responsible of listening to user input and triggering behaviors upon such events.
In terms of code, a `Keylogger` is basically a class conforming to the `Keylogger` abstract class.
In order to work across different platform, all keylogger implementation must inherit from the `Keylogger` class.

##### The Keylogger abstract
The `Keylogger` class provides a generic abstraction for every keylogger implementation.

```cpp
class KeyLogger
{
public:
	using MouseMoveCallback = std::function<void(spi::proto::MouseMove &&)>;
	using KeyPressCallback = std::function<void(spi::proto::KeyEvent &&)>;
	using MouseClickCallback = std::function<void(spi::proto::MouseClick &&)>;
	using WindowChangeCallback = std::function<void(spi::proto::WindowChanged &&)>;

	virtual bool setup() noexcept = 0;
	virtual void run() = 0;
	virtual void stop() = 0;

	void onMouseMoveEvent(MouseMoveCallback &&callback) noexcept;
	void onMouseClickEvent(MouseClickCallback &&callback) noexcept;
	void onKeyboardEvent(KeyPressCallback &&callback) noexcept;
	void onWindowChangeEvent(WindowChangeCallback &&callback) noexcept;

	virtual ~KeyLogger() noexcept = default;

protected:
	logging::Logger _log{"keylogger", logging::Level::Debug};
	MouseMoveCallback _mouseMoveCallback;
	MouseClickCallback _mouseClickCallback;
	KeyPressCallback _keyPressCallback;
	WindowChangeCallback _windowChangeCallback;
};
```

At program startup, the `setup` method shall be called. It should return `true` to indicate module readiness, or `false` otherwise.
After that, the callback setters shall be called by the main program with the appropriate data.


The `run` method shall now be called to start the keylogger and set it to the active state.

When the Keylogger is active, its core functionality is to listen to user input and call the appropriate callbacks.

The `run` and `stop` methods can be called at any time to set the keylogger to active and inactive states respectively.
