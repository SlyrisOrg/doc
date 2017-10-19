### Utils

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