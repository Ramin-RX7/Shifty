# Builtins: Classes:

Built-in classes may have more control over their objects and can have their own structure of `objects mapping`.\
No method/attribute can be overwritten in builtin types. Even classes that inherit from them.

## List of built-in types/classes/instances:


## boolean

Boolean is a type that only has two instances of `true` and `false`. These two are the way to detemine wether a condition is met or not.
Both of these instances can be directly used in the code but no trace of `Boolean` itself can be seen in the code.

> (Waiting for decision) Boolean must be implemented by enums instead of types. (As this needs more deep thoughts, no blueprint implementation of Boolean will be defined now.)

All conditions (e.g if-else, while) will implicitely be casted to Boolean. This happens via `bool` function mentioned above.
This casting is possible to fail as some types might not implement casting to `Boolean`.



## null

`null` is used to define a variable that does not hold a value. Essentially it shows the lack of value. The usage of this comes in handy in conjuction with `Optional`s where a certain operation might result in error but needs to be caught.

> `null` can be defined with an enum that contains only `null`.

Although the usage of null is not the same as `false` at all, `null` has a falsy value means in conditions it is converted to `false`. Also `null` is equal to itself only. `null` keyword can be used directly in the code.



## Integer

(Primitive type) Integer type (128-bit) can hold integer types. Any optimizations by the language is allowed, 128-bit is only the limitation range.

**Meta methods:**

    Constructor(object:Primitive) -> Integer {...};
    Equals ->  "true" only if both numbers are equal
    Copy   ->  A new Integer object of same number

**Casting methods:**

    String -> Same number but in String format
    Float  -> Same number but in Float format (adds `.0` to make it float)
    Iterable -> Send it as first positional argument of Iterable constructor.



## Float

(Primitive type) Float type

**Meta methods:**

    Constructor(object:Primitive) -> Float {...};
    Equals ->  "true" only if both numbers are equal
    Copy   ->  A new Integer object of same number

**Casting methods:**

    String   ->  Same number but in String format
    Integer  ->  Same number but in Integer format (Removes all decimal points)
    Iterable ->  Send it as first positional argument of Iterable constructor.



## String

(Primitive type) Strings are sequence of characters. They are usefull when dealing with stdout, text, user-input, files. etc.

**Meta methods:**

    Constructor(object) -> String {...};
    Equals ->  "true" only if both Strings contains same characters in the same order
    Copy   ->  A new String object of the same characters
    Iter   ->  Return each character of strings.
    Get    ->  Gets the character in given index (String indexes can only be Integers)
    Set    ->  Sets the corresponding index to given character/String
    Includes ->  Checks if a String is in the object

**Casting methods:**

    Integer -> (Might fail) Same String but in Integer format.
    Float   -> (Might fail) Same String but in Float format. (adds `.0` to make it if it's integer like string)

