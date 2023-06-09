# Storing Variables


To store variables we use 2 different mappings. One for objects and one for variables.


In objects mapping first we generate a unique id, this id will be the key. The value is a mapping shown below.

*Objects Mapping:*

    "id" = Mapping:
                "value" =  Mapping:  // data of the instance (based on type)
                                "attributes" =  Mapping:
                                                    name = id
                                "methods"    =  Mapping:
                                                    name = id
                "lock"  =  bool      // if the value is locked for access
                "const" =  bool      // if the value is a constant


In variables mapping each variable should point to an id or another variable.

*Variables Mapping:*

    name = Mapping:
                "scope" = scope_name
                "id" = id


When there are no variables in `variables mapping` that points to a specific object, the object will be deleted.


## Demonstration of how this works in action

Let's say both "a" and "b" are variables pointing to the same object.\
When "a" changes something in it's object, because "b" refers to the same memory location, the value of "b" also changes. if "a" is deleted (for any reason)(like manually or coming out of scope), "b" still points to the location it used to point and object remains in the memory.



## Pointers

Pointers are a way of setting variables value, where the variable will point to the same object that another variable point to.
When setting pointer of a variable as another variables value, basically what happends is that the `id` of the former will be set as the `id` of the defining variable.

(*This is not the same as c++ pointers where a variable can holds the memory address of another variable of a specific type. No such thing as a pointer variable exist*)

Different use of this:
- When sending them as a function argument, the actual object will be sent.
- When trying to set a new value to a variable but still need previous object it used to hold.



## Making copy of a variable

Whenever a variable is set to another variable's name, a copy of that will be taken and set to the new variable.
This act needs implementation of `copy` special method in variables type/class definition.
Default implementation of copy (in `type` class) is to return an instance of the same type, with copying (deep-copying) attributes and methods of the object.

