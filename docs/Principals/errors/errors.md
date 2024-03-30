# Errors

In this language, we use class-based hierarchy for our error classes. This means all errors are an object of a class that inherit from `BaseError`. Only objects that their type/class inherit from `BaseError` can be thrown.\

> This means the root class of error hierarchy is `BaseError`

Any error that is not caught, will terminate the program (read more about error handling [here](/docs/Principals/errors/error_handling.md)).



## Attributes

  - `message`: message shown to user when error is thrown
  - `cause`: The underlying cause of the error (null or another error instance).
  - `catchable`: (class attribute) Flag indicating whether the error can be caught with a catch block.


### auto populated attributes
Beside the mentioned attributes, some other attributes are sent to the error instance when they are raised.

  - `timestamp`: The timestamp when the error was raised.
  - `call_stack`: (described below)

All error instances will have an attribute called `call_stack` which is automatically populated by the language when the error is thrown.
This happens before any checks for error handling. which means it can be used in the `catch` blocks and `FailSafe` values.
Some advantages of this:
  - Help developer debug the error in catch block
  - Can be used to customize the error message by developer
  - Developer can raise another error with having the same call stack

> `Objects mapping`, `Variables mapping`, `Factories mapping` are also like call stack, but a flag determines whether they must be given to the instance when error is raised or not.



## Naming conventions
  - Short and describable
  - `Error` at then end of them



## BaseError

As said previously, all errors inherit from `BaseError`. `BaseError` is an abstract class (which means can not be instanciated) with having some default attributes/behavior set for the children classes.


### Error are false as booleans

All error objects always have a false boolean value. This can not be overwritten.


### Error are catchable

BaseError has the `catchable = true` which means any class inheriting from it will be catchable unless it sets the `catchable` explicitely to `false`.


### Language mappings are not given by default

Due to inefficient task of sending and keeping all 3 mappings to an instance (and also less importance), BaseError sets these attributes to false so mapping will not be sent.
- objects_mapping
- variables_mapping
- factories_mapping


### Error classes hierarchy

(Read more about each class in [builtin errors](/docs/Principals/builtins/errors.md) docs)

+ Validation:
  - InvalidValue
  - InvalidType
    * Casting:
      + NotImplementedCasting
      + ImplicitCasting

+ Lookup:
  - Name
  - Key:
    * Index
  - Attribute
  - ModuleNotFound
  - Reference

+ PermissionError
  - ConstantModification
  - FinalOverride
  - FactoryRedefinition
  - FactoryNameConflict

+ Syntax
+ Internal
+ KeyboardInterrupt
+ Recursion
+ Timeout
+ Assertion
+ EndOfIteration
