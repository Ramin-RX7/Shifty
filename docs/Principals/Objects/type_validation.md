# Type Validation

In [types](/docs/principals/objects/types.md) we talked about `Unions` (and `Type Aliases`).
In this section we talk about how Unions and other types like them actually work under the hood

All of the classes that want to take place in type validation situations must inherit from `Conditional` class.

Beside `Union` there are several other classes that help type validation and type grouping.



## Optional

This type either a value of required type must be given or either `null`.

This means in

```shifty
func f(x:Optional(String)){
    ...
}
```

In each call to `f`, the `x` argument must have a `String` type or must be `null`.

> This is just another way of writing `Union(String,null)` so basically `Optional` is shortcut for nullable variables.


## Supports

`Supports` checks if the given argument type supports a certain attribute/method publicly.

example:

```shifty
func f(x:Supports("mymethod")){
    ...
}
```

This means in each call to `f`, `x` must have a type that has a `mymethod` that can be accessed from outside of the class.


## Castable

`Castable` checks if the argument given type can be casted to the defined type(s).
