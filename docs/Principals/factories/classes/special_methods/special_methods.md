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
- **copy**: returns the new object when taking a copy of the object
- **constructor**: used to initialize the instance
- **destructor**: used for cleanups when the instance is being deleted from memory.

> (waiting for decision) Should there be a method to initialize the instance implicitly when a variable is declared but not initialized by the user? if the language allow user to declare a variable without explicitely initializing it, this feature must exist.

read more about `meta-methods` [here](/docs/principals/factories/classes/special_methods/metas.md)



## Operator Methods

these methods handle how instances should behave when used in different operators.

Some of binary operators:
- "**+**"
- "**-**"
- "**\***"
- "**/**"

Some of unary operators:
- "**!**"

> Need decision to be made: `@ $ % ^ & * - ~`

read more about `operator-methods` [here](/docs/principals/factories/classes/special_methods/operators.md)



## Casting methods (Type conversion)

Casting methods let the class instance be converted to other types. This behavior is important as one of the key features of the language which is implicit casting uses these methods a lot.

read complete doc of `operator-methods` [here](/docs/principals/factories/classes/special_methods/casting.md)
