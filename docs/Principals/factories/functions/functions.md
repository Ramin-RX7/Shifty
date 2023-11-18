# Functions

Functions do not have access to any variables outside of them.

Table of accessibility in function bodies:

| NAME               | ACCESSIBILITY |
|:------------------:|:-------------:|
| *variables         | false         |
| *constants         | true          |
| functions          | true          |
| classes            | true          |
| (imported) modules | true          |

> *variables: this refers to instances (of any type) created outside of function body\
> *constants: even though constants are instances of a type, but their immutability makes them available to use in functions

Even though restricting variable access to functions makes them purer, there is a way to access objects within the function scope. This can happen when passing a reference as an argument to the function (This is explained in [Parameters](#parameters) section).

Function overloading will not be supported since functions must be able to only perform one task that can be done on any type of parameters they accept. In `f(x)` if `x` can be of both `MyClass` and `OtherClass`, main body of the function should not differ for each of these types. Instead the data that is needed from their instances must be mined on the first lines of the function via if-elif-else clause and the rest of the function must be the same. If function body differs for different types of parameters, a new function must be defined for that purpose.


## Parameters

When a function is called with arguments, a copy of all of the given arguments are created, then sent to the function.
So when the function executes, it will receive new (copied) objects which will be destroyed when the function returns.


### Reference parameters

When defining functions, it's possible to define a parameter that receives only reference.
This way you can manipulate with objects defined outside of the function.\
If a function parameter is set to accept references, when calling the function, only references are acceptable and normal variables will result in error.\
But when the parameter is declared normally, and in a certain call a reference is passed, not only no error will be raised but also the real object (not the copy of it), will be passed to the function.


### read-only parameters

These type of parameters sets the argument given in the function call `read-only`.
Which means the value they hold can not be changed in the function body.
This is useful with `Reference Paramters` as it guarantees that passing a reference of an object to the function will not change the value of it at all.

> (waiting for decision) Should `read-only` parameter be a guarantee by the language or by the function?
(by language makes it more sensible but it costs a lot of time to change reference object attributes to constant then switch them back. By function makes it less secure but it makes it much faster as no changes are needed)



---------------



## Functions execution

Function calls are handled by an object of a class called `Task`.
`Task` is a class that will be initialized whenever a factory with type of `function` is created. It will be saved in the factory `data` mapping. In fact, whenever the function is called, a method of the initilized object we just mentioned will be called.

    Constructor(code:string, parameters:Tuple[Dictionary], variadic:String|null, return_type:Factory) -> Task {
        base.init();
        // create mappings
    };

*__Note__: parameter `parameters` is a tuple with this structure*:

    [
        {
            "name" : PARAM_NAME,   // e.g: x
            "type" : PARAM_TYPE,   // e.g: Integer
        },
        {
            "name" : PARAM_NAME,       // e.g: y
            "type" : PARAM_TYPE,       // e.g: Float
            "default": DEFAULT_VALUE   // e.g: 10.0
        },
    ]

When a function call is then received, a method of this Task object must be called which needs to follow these steps in order to obtain the result of the function:

- Validate given arguments:
  + validate if required arguements are all given
  + validate if their type is acceptable
- Perform type casting action on arguments that need to be casted
- Update the OM and VM of the function based on new arguments
- Parse the code (body) of the function and run it.
- Check for correct return type
- return the value to the user
