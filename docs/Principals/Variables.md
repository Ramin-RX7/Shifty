# Storing Vars


To store variables we use 2 different mappings. One for objects and one for variables.


In objects mapping first we generate a unique id, this id will be the key. The value is a mapping shown below.

*Objects Mapping:*

    id = Mapping:
            "value" =  Mapping:  // instance of a class stored in the variable
                            "attributes" =  Mapping:
                                                name = id
                            "methods"    =  Mapping:
                                                name = id
            "lock"  =  bool      // if the value is locked for access
            "const" =  bool      // if the value is a constant


In variables mapping each variable should point to an id or another variable.

*Variables Mapping:*

    name = Mapping:
                "id" = id
                // or
                "variable" = name



## Demonstration of how this works in action

Let's say both "a" and "b" are variables pointing to the same object. when "a" changes something in it's object, because "b" refers to the same memory location, the value of "b" also changes. if "a" is deleted (for any reason)(like manually or coming out of scope), "b" still points to the location it used to point and object remains in the memory

But when we have "a" and "b" variable where "a" points to an object but "b" points to "a", even though all changes to "a" also change "b" and same thing goes the opposite way around but here when "a" is deleted (for any reason), then "b" is also deleted. And now because there are no variables in "variables mapping" that points to the object "a" used to refer, the object is deleted.
