### core/utils

**utils** provides a bunch of miscellaneous utilities.
All of them are part of the `utils` namespace.

##### endian
The `endian` function allows detecting platform endianness.

```cpp
Endian endian() noexcept
```

##### ENUM
The `ENUM` macro allows preprocessor-based generation of reflective enumerations.
These enumerations can be easily converted back and forth to strings.
It is also possible to iterate through the available values of such an enumeration type.

```cpp
ENUM(AnEnum, VALUE_A, VALUE_B);

AnEnum v(AnEnum::VALUE_A);
//v is now AnEnum::VALUE_A

v = AnEnum::VALUE_B;
//v is now AnEnum::VALUE_B

std::string str = v.toString();
//str is now "VALUE_B"

AnEnum s("VALUE_A");
//s is now AnEnum::VALUE_A

for (const auto &cur : AnEnum::values()) {
    //Do stuff
}
```

##### Guard
`Guard` is a template scope-guarded class to adopt RAII-like behavior on objects that don't support it natively (for example, raw C objects)

```cpp
template <typename T>
class Guard;
```
```cpp
void doStuff()
{
    utils::Guard<int> sock(::socket(AF_INET, SOCK_STREAM, 0, ::close);
    //sock is destroyed automatically when it goes out of scope

    if (someCall()) {
        return ;
    }
    [...]
}
```

##### NonCopyable
The `NonCopyable` class can be inherited from in order to prevent copying of a object.

##### NonMovable
The `NonMovable` class can be inherited from in order to prevent moving of a object.

##### Relational
The `Relational` class can be inherited from in order to simplify implementation of relational operators (`<`, `>`, `<=`, `=>`, `==`, `!=`).
The inheriting class only needs to define the `<` and `=` operators.

##### Singleton
The `Singleton` class can be inherited from to allow creating a unique shared instance of the inheriting class.
The instance can be accessed through the `get` static member function, and will be created on the first request.
