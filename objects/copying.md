# Making copy of a variable

Whenever a variable is set to another variable's name, a copy of that will be taken and set to the new variable.
This act needs implementation of `copy` special method in variables type/class definition.
Default implementation of copy (in `type` class) is to copy the actual object in `objects mapping` and return a reference to that (which happens in the language that our language is implemented). This will not only be a full copy (deep copy) of the actual object but also an efficient way. In deep copy all attributes will be redefined and no reference will remain the same as the old object.

```
// Example:
a = 5
b = a      // This will take a copy of `a`
b += 1     // now `b` equals to 6 and `a` remains 5
```
# Copying complex types

Since there are several user defined types (imprimitive) that hold multiple attributes (which they can also be other complex objects), when we try to copy an object, we must go through the OMV of it, get all the attributes of it and then check if they are primitive, copy them easily and set them on the new instance but if they are not primitive, the same logic must be done over and over again on their OMV in order to finalize the copying logic.
# Why copying is useful

The main reason and usage of copying comes in function calls. When passing a variable/object directly to the function, the object/variable itself is not actually sent, but the object they are pointing to (OMV) is copied (with the logic explained above) and then the new copy is sent to the function.
This ensures data consistency and prevents unknown data changes on the real object.

> Yet there are [[references]] which allows bypassing this in order to change the object itself in the required places

