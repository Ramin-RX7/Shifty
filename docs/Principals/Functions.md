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

Even though restricting variable access to functions makes them purer, there is a way to access objects within the function scope. This can happen when passing a pointer as an argument to the function (This is explained in [Parameters](#parameters) section).



## Parameters

When a function is called with arguments, a copy of all of the given arguments are created, then sent to the function.
So when the function executes, it will receive new (copied) objects which will be destroyed when the function returns.

### Pointer parameters

When defining functions, it's possible to define a parameter that receives only pointers.
This way you can manipulate with objects defined outside of the function.\
If a function parameter is set to accept pointers, when calling the function, pointers **must** be passed (If the variable is passed normally, it will raise error.)\
But when the parameter is declared normally, and in a certain call a pointer is passed, not only no error will be raised but also the real object (not the copy of it), will be used in the function body.
