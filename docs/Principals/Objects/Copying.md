## Making copy of a variable

Whenever a variable is set to another variable's name, a copy of that will be taken and set to the new variable.
This act needs implementation of `copy` special method in variables type/class definition.
Default implementation of copy (in `type` class) is to copy the actual object in `objects mapping` and return a reference to that (which happens in the language that our language is implemented). This will not only be a full copy (deep copy) of the actual object but also an efficient way. In deep copy all attributes will be redefined and no reference will remain the same as the old object.

    // Example:
    a = 5
    b = a      // This will take a copy of `a`
    b += 1     // now `b` equals to 6 and `a` remains 5
