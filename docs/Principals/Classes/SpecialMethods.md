# Classes: Special methods

Special methods refers to several types of methods it self.
Each of these types of methods are explained in their corresponding section.



## Meta methods

These methods are the ones to handle and manipulate the instance of the class in different use cases.

list of methods:

- **equals**: when using "**`==`**" operator
- **get**: when using "instance`[item]`" (this also works on slices)
- **set**: when using "**instance[item] = ...**"
- **hash**: to get a hash of the instance (this should method will be used when `equals` is not defined)
- **includes**: used in "`in`" expression.
- **iter**: will be called in each iteration of for loop
- **call**: when instance is called



## Operator Methods

these methods handle how instances should behave when used in different operators.

List of binary operators:
- "**+**"
- "**-**"
- "**\***"
- "**/**"

List of unary operators:
- "**!**"

> Need decision to be made: `@ $ % ^ & * - ~`



## Casting methods (Type conversion)

Third group includes methods that handle how to cast instances of other classes into this class.\
When working with functions sometimes may a call comes with wrong argument types. let's say we have `f(x)` where `x` must be of type `MyClass`. if we call `f` with a instance of `OtherClass` as x argument, we must get an error. But because `MyClass` has implemented the casting method for `OtherClass` instances, `x` argument we sent will be converted to `MyClass` and the program keeps working correctly.

**NOT IMPLEMENTED (Waiting for decision):**\
*Outgoing Casting*: With this new way of casting, not only you can set how to cast from another type to this class, but also how to cast from this class to another.\
Question: when we have 2 different classes "A" and "B", if "A" needs to be casted to "B" and "A" has implemented the method to convert to "B" but also "B" has implemented method to recieve from "A", What should happen?

    1: Only receiver should work
    2: Only sender should work
    3: Both receiver and sender should work (order is important)
    4: Error should occur