# Classes (Types)

All classes inherit from default `type` class that is already implemented in the language.





In order to be displayed in the output, classes should implement `str` method. This method **should** return string

Default implementation for `str` method returns `${objectType}::${objectId}`  (implemented in `type` class)


## Special methods

Special methods are inspired by python dunder methods.
These methods implement extra bits to objects.

(These methods may vary in different languages)



## Casting

When working with functions sometimes may a call comes with wrong argument types. For situations like this, classes can implement a method which will convert their object to the corresponding class when facing errors like this. Also all classes can implement a method which will try to convert given type to their own selves.

**NOT IMPLEMENTED:**
when we have 2 different classes "A" and "B", if "A" needs to be casted to "B" and "A" has implemented the method to convert to "B" but also "B" has implemented method to recieve from "A", What should happen?

    1: Only receiver should work
    2: Only sender should work
    3: Both receiver and sender should work (order is important)
    4: Error should occur
