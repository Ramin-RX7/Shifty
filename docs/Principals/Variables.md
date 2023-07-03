# Storing Variables


To store variables we use 2 different mappings. One for objects and one for variables.


In objects mapping first we generate a unique id, this id will be the key. The data is a mapping shown below.

*Objects Mapping:*

    id = Mapping:
                "data" =  Mapping:  // data of the instance (based on type)
                                "attributes" =  Mapping:
                                                    name = id
                                "methods"    =  Mapping:
                                                    name = id
                "lock"  =  bool      // if the object is locked for access
                "const" =  bool      // if the object/variable is a constant


In variables mapping each variable should point to an id or another variable.

*Variables Mapping:*

    name = Mapping:
                "scope" = scope_name
                "id" = id


For each object in `Objects mapping` if there won't be at least one variable pointing to it, it will be deleted.


### Demonstration of how this works in action

> Let's say both "a" and "b" are variables pointing to the same object.\
> When "a" changes something in it's object, because "b" refers to the same memory location, the value of "b" also changes.\
> if "a" is deleted (for any reason)(like manually or coming out of scope), "b" still points to the location it used to point so object remains in the memory.



## Declaring variable type

Variables must be initialized in their declaration time.\
Variables are not forced to explicitly define their type in declaration.\
function parameters must declare their type.\
function return type is neccessarily but can be dropped in syntax if no return is in the function.



## References

Refrences are a way of getting the object a variable is pointing to.
When setting reference of a variable as another variables value, basically what happens is that the `id` of the former will be set as the `id` of the defining variable. So any changes to either of them (changes in object) will also affect the other one.

(*This differs from c++ references at some points.*)

Different use of this:\
    &nbsp; &nbsp; When sending them as a function argument, the actual object will be sent. (read more [here](/docs/principals/Functions.md/#parameters))\
    &nbsp; &nbsp; When trying to set a new value to a variable but still need previous.\
    &nbsp; &nbsp; When we want to make an alias for a variable

    // Example:
    a = 5
    b = &a     // suppose `&` makes a reference of variable in our language
    b += 1     // as both `a` and `b` points to same object, now both of them are equal to 6



## Constants

Constants are a kind of variable/objects that will not change after their declaration.
As you saw in the `objects mapping`, there is a key called `const` which indicates wether the data of the object can be changed or not.
Now how does this protect variables if we redeclare one? Well, when trying to declare a variable, first thing that is checked is that if a variable with the same name is defined or not. if defined, then the object it holds is checked to see if it is a constant variable or not. if it's a constant, then error should be raised.\
Though this protects the variable, still the object `data` is not protected.
This is handled when trying to initialize a variable as a constant. All attributes it holds will set as constant in their objects, which will block any attempts to change the objects defined in the base object.\
Problem with constants comes with using them together with references. If an attribute of a constant is a reference to another object, this means that attribute will not be set as constant and it might change later on. Although this should not raise error since references are always used explicitly, but this should show a warning to the user as the constant variable/object is not really constant (due to the use of this reference). If the given reference object is a constant by it self, no changes can be done in the new object hence no warning will be shown.

    // e.g 1:
    const a = Person(firstname="Peter", lastname="Griffin")
    a.lastname = "Parker"   // this will raise error as the data is being changed
    a = 5   // this will also raise error as the constant variable is being redefined
    // e.g 2:
    name = "Peter"
    const a = Person(firstname=&name, lastname="Griffin")  // This should give user a warning as firstname is free to change.
    name += "..."  // now a.firstname is also "Peter..."



## Making copy of a variable

Whenever a variable is set to another variable's name, a copy of that will be taken and set to the new variable.
This act needs implementation of `copy` special method in variables type/class definition.
Default implementation of copy (in `type` class) is to return an instance of the same type, with copying (deep-copying) attributes and methods of the object.

    // Example:
    a = 5
    b = a      // This will take a copy of `a`
    b += 1     // now `b` equals to 6 and `a` remains 5



## Note about classes, functions and modules

Beside having 2 mappings for objects and variables, there's a mapping for the ones mentioned above called `Factories Mapping` with a structure defined below.

    Name = Mapping:
                "type" = type
                "data" = Mapping :
                            // This varies for each of them
                            // (Not implemented yet)

No variables are allowed to be created with a name that exists in this mapping. If a variable has already been created with a name and then a class/function/module with the same name is declared, error will be raised.




# Todo/Notes of this doc:

Scopes implementation

Check marks-and-sweep algorithm for garbage collection system

Some algorithms to stop cyclic references when using marks-and-sweep: Cheney's algorithm, Baker's algorithm, and the "two-finger" algorithm

**Object Pooling System**:

- Using object-pooling and concurrent garbage collection system at the same time (hybrid grabage collector)
- Users be able to set a flag when making classes to indicate wether objects of this class should be pooled in object pooling system or not.
- ? Using a fixed size object pooling system or dynamic sized?
- ? Let the size of the pool be configurable by user?
