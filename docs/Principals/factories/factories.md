# Builtins: Factories

Factories in this language are mostly called to objects that are mostly used to create new objects.

The behavior of them are also customizable in certain cases which makes them powerful.

Factories can not be defined twice in the code and redefinition of them result in _[FactoryRedefinitionError](/docs/Principals/builtins/errors.md/#factoryredefinitionerror)_. This happens when a factory is being created in a [factories mapping](./factories_mapping.md) that already contains another factory with similar name.




## Classes

For details about classes please refer to [Classes](/docs/Principals/factories/classes/classes.md) which is a dedicated part of documentation to classes

> All of the builtin methods are defined as final which means no method/attribute can be overwritten in builtin types. Even classes that inherit from them.




## Structs

They behave similar to classes but they are much simpler.\

They have a constructor that takes all attributes as arguments (can have default value) and set them to the corresponding instance attributes.

Inheriting from other structs is possible (but not recommended)


Differences between `Structs` and `Classes`:

- No methods can be defined in the `Structs`. They hold only attributes.
- No access control modifiers are in structs and all attributes are public.
- structs are immutable which means the value of an attribute an not be changed.

**Meta Methods**:

    Equals (`==`) -> only if two structs are the same type and their attribute values are the same.
    Copy -> Returns an struct of the same type with same attribute values.


**Casting Methods**:

    String -> A constructor like string.
    Mapping -> A set of key-value pairs by attribute name and it's corresponding value.


### why to use structs
- Structs are useful due to their immutability
- Structs can be used over mappings when a specific structure needs to be used (nothing more or less)



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

It's possible to set value for enum attributes. However this requires few conditions:
- All attributes must have a value. It's not possible to have a combination of value-associated and no-associated-value enums.
- All of the values must have the same type.

Breaking any of these two rules result in `InvalidTypeError`.


In the example below it is shown how enums associated with values can be helpful.

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




## Modules

Modules are a piece of code in another file just like any other code but they have their own mappings. Modules can be imported to the code. When they are imported all the code inside them will be executed and the name of the module will be set as the placeholder for all variables/factories that exist there. This means when you try to access something in a module, language has to lookup in the mappings of the module instead of program's main mappings.

    func f(x){
        return x
    }

    // suppose "my_module" is a module that also defines a factory/variable called `f`
    import my_module
    // now you can access the `f` function declared inside of `my_module`
    my_module.f(5)

It is possible to import a specific object from a module directly. When trying to import directly, it is important to know that:
- it does not have a name same as a factory
- it does not have a name same as a constant variable

You can also import all objects of a module directly but it is highly discourages.

> constants and factories are the reason which discourage mass direct imports in the language.
