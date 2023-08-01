# Classes: Methods: Casting methods


This group of methods includes the ones that handle how to cast instances of a class to another class.\

When working with functions sometimes may a call comes with wrong argument types. Let's say we have `f(x)` where `x` must be of type `MyClass`. If we call `f` with an instance of `OtherClass` as `x` argument, we must get an error. But because `OtherClass` has implemented the casting method to `MyClass` instance, `x` argument we sent will be converted to `MyClass` and the program keeps working correctly.


There are several rules when using these methods.

- A casting method has to return a value of the type it is being casted to. The return type is not overwritable.
- When the function parameter takes a reference, casting methods will not work (As the actual object is not sent to the function)
