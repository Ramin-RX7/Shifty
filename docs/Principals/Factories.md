# Builtins: Factories

Factories in this language are mostly called to things that can define a new data types.

The behavior of them are also customizable in certain cases which makes them powerful.

Factories can not be defined twice in the code and redefinition of them result in _[FactoryRedefinitionError](/docs/Principals/Builtins/Errors.md/#factoryredefinitionerror)_. This happens when a factory is being created in a `factories mapping` that already contains another factory with similar name.



## Classes

For details about classes please refer to [Classes](/docs/Principals/Classes/Classes.md) which is a dedicated part of documentation to classes

> No method/attribute can be overwritten in builtin types. Even classes that inherit from them.


## Structs

They behave similar to classes but they are much simpler.\

They have a constructor that takes all attributes as arguments (can have default value) and set them to the corresponding instance attributes.

Differences between `Structs` and `Classes`:

- No methods can be defined in the `Structs`. They hold only attributes.
- No access control modifiers are in structs and all attributes are public.

Equals (`==`) behavior on structs:
    only if two structs are the same type and their attribute values are the same.

Copy:
    Returns an struct of the same type with same attribute values.


**Casting Methods**:

    String -> A constructor like string.
    Dictionary -> A set of key-value pairs by attribute name and it's corresponding value.



## Enums

Enums are used to define a set of named constants representing distinct, unique values with a specific underlying data type.

When there are only limited number of instances of a type and all of them are also known, we can use enums. A simple example is an enum for different directions:

    Enum Directrion {
        up,
        down,
        left,
        right
    }

    // Accessing the attributes
    Direction.left
    stdout(Direction.up)  -->  "Direction::up"

As you can see, the attributes do not hold a value (these are called no-associated-value enums). The reason behind this is that the attribute name itself is also the value of itself. The attributes of enums must be straight forward to what they actually mean. If an attribute is possible to have different values, it means that enums are not suitable for that situation.\

Enums are all immutable (not constant). This means they can not be changed (just like tuples).

It's possible to define methods for enums.

The type of all attributes of the enum is the name of the enum.



### Simple example of using classes, enums and structs together

> This is not the real syntax of the language. It's just a demonstration of how these can work together

    Struct Color {
        red,
        green,
        blud
    }

    Enum PhoneBrand {
        Apple,
        Samsung,
        Nokia
    }


    class phone {
        constructor(brand:PhoneBrand, color:Color){
            ...
        }
    }


> Note: in the example below it is shown how enums associated with values can be helpful.

    Enum PhoneColor {
        black = Color(0,0,0),
        white = Color(255,255,255),
        red = Color(255,0,0),
        blue = Color(0,0,255),
        yellow = Color(255,255,0),
    }

    class Phone {
        constructor(brand:PhoneBrand, color:PhoneColor){
            ...
        }
    }

> (Wainting for decision) Enums can have assigned values to their attributes.
> - Rules of having this beside simple enums:
>   1. All of their values must have same type
>   2. An enum must either set a value for all of it attributes or none of them.
