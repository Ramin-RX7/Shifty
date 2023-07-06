# Types

All objects have a type. Their type is the class they are initialized by. As the language must not have a restriction for redefining a variable, sometimes it is useful to be able to get a variable/object type (e.g in tests). Different types can have different attributes/methods but they also may have some attributes/methods with the same name. With this approach, some types can be grouped together and be used in a situation where the type does not matter, but their behavior (attributes/methods) are the main subject.

> Though this document might be related to classes and must be mentioned in Classes section, functions parameter and return types also make their way into this topic too. This will lead to this situation where Types have their own doc indepenent from Classes and Function.


## Unions

Function parameters are not strictly typed, but if their type is specified in their signature then it is important to verify each call to the function comes with correct argument type. If a function parameter wants to accept several types, or a particular function wants to have different return types (based on given arguments), `Unions` will come in handy.\
Unions are a way to set multiple acceptable types to variables.
> Having Union return type for functions is discouraged (but not disallowed).

    // Example 1: parameter
    func f(x) {...}               // x can be of any type
    func f(x:int) {...}           // x can be only 'int'
    func f(x:int|float) {...}     // x can be either of 'int' or 'float'

    // Example 2: return
    func f(x) {...}                  // can return any type
    func f(x) -> int {...}           // only returns an instance of int
    func f(x) -> int|float {...}     // only return an int or a float
> The syntax used above for Unions is just for example purposes (since syntax of the language is not implemented yet)

Unions are a type themselves and there can be instances of them. This means a function parameter can accept only Unions as it's type (if useful in any case). Read more about Union class in it's own documentation.


## Type Aliases

When different types share similar attributes/methods we can group them together. This usually happens in function parameters that only need a specific part of an instance so their type does not really matter.\
Let's say we have a fucntion called `f` with parameter `x` where `x` can be an `int` or a `float`. This could easily be done using Unions:

    func f(x:int|float){...}

But it is clear that not only this will make code less readable but also the same thing can happen in so many functions. In this situation `Type-aliases` helps us with writing less code on the side of a more readable code.\
Type aliases are *variables* that hold `Union` objects. A simple example is given below

    Number =  int | float
    func f(x:Number) -> Number {...}

Here we define a type-alias variable for the types that are numbers, called `Number` which points to a Union instance that holds `int` and `float`.\
In the next line, the `x` parameter in `f` accepts instances of type `Number` which means it can take instances of either `int` and `float`. Also the return type is `Number` which means it will be either an `int` or a `float`.\
Note that this is the same as Unions where using uncertain return type is discouraged (but not disallowed).

So basically type aliases work the same as Unions but the difference is that the Union is an object type itself, while Type-Alias is what we call a variable that points to an Union object.
