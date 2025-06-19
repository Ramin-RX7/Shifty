# Classes (Types)

Classes are (Probably) the most used factory in the language. User can define classes to make instances of them and use their attributes and methods

> No more general info about classes are provided here, only language-specific parts!

Classes can have class variables/attributes which is a shared attribute accross all instances.

All classes inherit from default `type` class that is already implemented in the language.

As the instances might be needed to be shown in the output, classes should implement `Cast:String` method for them.\
Default implementation for `Cast:String` method returns `${objectType}::${objectId}`  (implemented in `type` class)\
(read more in [Casting](/docs/principals/factories/classes/special_methods/special_methods.md#casting-methods-type-conversion))



## Access control modifiers

attributes and methods can be either public or private (they must be public by default).\
Public attributes/methods can be accesses from anywhere in the code but private ones can only be accessed in the class body.\
If a class inherit from another class with a private attribute, child class can have access to the private attribute, though it can not change the visibility of it. The same thing goes for public ones which the child class can not change their visibility.\

### (Waiting for decision) Shilded attributes

Using this access modifier will limit the attribute modification to the class body. Outside of the class body, these attributes can only be retrieved but not changed.


## Methods

Methods are separately documented in [methods](/docs/principals/factories/classes/methods.md)
