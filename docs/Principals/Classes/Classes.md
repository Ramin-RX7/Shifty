# Classes (Types)

Classes are (Probably) the most used factory in the language. User can define classes to make instances of them and use their attributes and methods

> No more general info about classes are provided here, only language-specific parts!


Attributes can only be set in the class and no new attribute can be defined outside of the body (This does not mean the values of the attributes can not change).

Classes can have class variables/attributes which is a shared attribute accross all instances. These attributes are all read-only for the instances and their value can only be changed in the class body.

All classes inherit from default `type` class that is already implemented in the language.

As the instances might be needed to be shown in the output, classes should implement `Cast:String` method for them.\
Default implementation for `Cast:String` method returns `${objectType}::${objectId}`  (implemented in `type` class)\
(read more in [Casting](/docs/principals/Classes/SpecialMethods.md#casting-methods-type-conversion))



## Access control modifiers

attributes and methods can be either public or private (they must be public by default).\
Public attributes/methods can be accesses from anywhere in the code but private ones can only be accessed in the class body.\
If a class inherit from another class with a private attribute, child class can have access to the private attribute, though it can not change the visibility of it. The same thing goes for public ones which the child class can not change their visibility.\

> Static methods can not be private





## Methods

### instance methods

(No general explaination) All normal functions defined in class body will be treated as instance methods.
The `self` argument must be sent to the function automatically by the language and must not be seen in the method signature.


### class methods

Class methods are associated with the class itself rather than instances.\
Functions defined in the class body with a special `class method` sign (implemented in the syntax), are not accessible by instances and instead, the name of the class is required to be able to use them from outside of the class (if they are public).


### static methods

Static methods are not associated with instances or the class itself. They can work independently even if we take them outside of the class. But as they are only used within the class related functionalities, they are defined in the class. (The syntax must be like class-methods)


### Special methods

Special methods are related to class behavior in more general purposes.
These methods implement extra bits to objects.
> They are documented in the [SpecialMethods.md](/docs/principals/Classes/SpecialMethods.md)
