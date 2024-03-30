# Builtins: Errors

The following error classes represent various runtime issues and are built-in within the language.\
Each class corresponds to a specific error scenario that might arise during program execution.\
When utilizing the built-in features, any coding errors should trigger the appropriate error type.

For all the built-in thrown errors, it's essential to provide a user-friendly message using the `message` attribute. Although there's an option to include objects, variables, and factories mappings within the errors, the default setting for all built-in errors is to have these mappings flagged as `false`.

Below is the list of these built-in error classes.




# BaseError

The foundation of the error classes hierarchy is the `BaseError` class. When attempting to throw an error, the first check is whether it's derived from `BaseError`. While this error is not thrown by the language itself, it serves as a foundation to create other types of errors. Users can also manually throw errors of this type.

    class BaseError {
        catchable = True

        objects_mapping = false
        variables_mapping = false
        factories_mapping = false

        constructor(message:str){
            base.init()
        }

        {cast}Boolean(){
            return false
        }
        {cast}String(){
            return typeof(self).name + ": " + self.message
        }
    }



## ValidationError
_derived from [BaseError](#baseerror)_

Thrown when a validation fails. It is used when a data input is unknown and when it is recieved, validations on it fails. This class is mostly supposed to be derived by other classes (like InvalidValueError and InvalidTypeError) but still enough for some errors.


## InvalidTypeError
_derived from [ValidationError](#validationerror)_

This error is thrown when an invalid type is provided, typically occurring in function calls.
It's important to note that `InvalidTypeError` should not be confused with `CastingError`. The `InvalidTypeError` can arise when working with Unions or other validation scenarios where a type is expected to implement a certain method or fulfill a specific condition but fails to do so.


## CastingError
_derived from [InvalidTypeError](#invalidtypeerror)_

The `CastingError` type of error is associated with issues related to casting. While this error is not directly utilized by the language, users can employ it when necessary.\
The existence of this error class is mainly to serve as the base class for `ImplicitCastingError` and `NotImplementedCastingError`, allowing users to catch both error types simultaneously.


## ImplicitCastingError
_derived from [CastingError](#castingerror)_

The `ImplicitCastingError` is thrown when a type is provided in a function call that is incorrect, prompting the language to attempt an implicit cast to the required type. This error is raised when the necessary casting method is not defined in the given object type.


## NotImplementedCastingError
_derived from [CastingError](#castingerror)_

This error is raised when a user attempts to explicitly cast one type to another using the `.as()` method, but the requested type is not supported by the current type's casting methods.


## InvalidValueError
_derived from [ValidationError](#validationerror)_

The InvalidValueError is raised when a value is not valid for a specific parameter or context. This error type is intended to be used when the issue lies with the value of the object, rather than its type.\
For instance, this error can be utilized when a parameter must fall within a certain range, but the provided value does not meet this requirement.\
While this error can serve as a general category, it can also be further specialized by deriving more specific error classes to convey the exact nature of the value validation error.



## LookupError
_derived from [BaseError](#baseerror)_

This serves as a foundational class for errors stemming from actions that involve lookups. Errors like `NameError`, `AttributeError`, and `IndexError` fall under this category. They occur when the language attempts to locate a corresponding name, attribute, or index, but fails to do so. This error hierarchy captures situations where the required lookup fails to match an existing entity.


## NameError
_derived from [LookupError](#lookuperror)_

This error occurs when a user attempts to access a variable that has not been defined in the current `variables mapping`. It is less likely to see this error be thrown by user (as it is meant to be used for variable names lookups).


## KeyError
_derived from [LookupError](#lookuperror)_

The KeyError has to be raised when an attempt is made to use the `Meta:get` method, which involves accessing a key in an object (using `myvar[key]`), but the specified key is not found in the object's structure.


## IndexError
_derived from [KeyError](#keyeerror)_

The `IndexError` is raised when an attempt is made to access an index on an object that does not exist. This error occurs when working with objects that have indexed elements, such as arrays or lists, and an out-of-bounds index is provided. The `IndexError` is a subcategory of the broader KeyError and LookupError hierarchy since it is raised due to invalid use of `Meta:get`


## AttributeError
_derived from [LookupError](#lookuperror)_

The `AttributeError` is raised when an attempt is made to access an attribute on an object that does not exist within its type. This commonly occurs when trying to access attributes/methods that the object's class does not have.


## ModuleNotFoundError
_derived from [LookupError](#lookuperror)_

This error is thrown when trying to import a module that does not exist.


## DanglingReferenceError
_derived from [LookupError](#lookuperror)_

In some rare cases a variable in `variables mapping` can point to an object id that no longer exists in the `objects mapping`. When trying to access that variable, the `DanglingReferenceError` is thrown (since the object can not be found in the objects mapping).



## PermissionError
_derived from [BaseError](#baseerror)_

This error is raised when attempting to perform actions that violate required conditions. It serves as a base class for errors associated with permission-related violations, such as redefining a factory, modifying a constant, overriding a final method, or attempting actions that are not allowed in specific contexts.\
`PermissionError` is typically meant to be derived by other classes and is less commonly used directly.


## ConstantModificationError
_derived from [PermissionError](#permissionerror)_

This error is thrown when user tries to modify a constant variable/object value.


## FactoryRedefinitionError
_derived from [PermissionError](#permissionerror)_

This error is thrown when trying to define a factory with a name that exists in the current `factories mapping`.


## FactoryNameConflictError
_derived from [PermissionError](#permissionerror)_

This error is raised when a factory is declared with a name that already exists in the `variables mapping`


## FinalOverrideError
_derived from [PermissionError](#permissionerror)_

This error is thrown when a class overrides a method that has a final definition in the parent classes.



## SyntaxError
_derived from [BaseError](#baseerror)_

This error is thrown when a syntax error is detected in the code.


## InternalError
_derived from [BaseError](#baseerror)_

Thrown when an internal problem has caused the damage and terminated the program. When any problem occurs in the background (not related to users code), but still the program can not continue, this has to be raised before termination


## KeyboardInterruptError
_derived from [BaseError](#baseerror)_

This error is thrown when keyboard interrupt has been detected.


## RecursionError
_derived from [BaseError](#baseerror)_

This error is thrown when language detects the maximum recursion depth is exceeded.


## TimeoutError
_derived from [BaseError](#baseerror)_

Thrown when an action has taken longer than it should.


## AssertionError
_derived from [BaseError](#baseerror)_

This error is thrown when an `assert` statement fails.


## EndOfIterationError
_derived from [BaseError](#baseerror)_

This error is thrown when an iterator has been completely iterated through so the `for` loop understands the loop has ended
