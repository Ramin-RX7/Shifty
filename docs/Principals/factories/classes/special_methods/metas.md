# Classes: Methods: Meta methods

`Meta-methods` are methods that handle/manipulate the instance of the class in different use cases in the language.\
These methods play special role in implementing different kinds of data types.\
Some key features can be directly use by the language without the user needing to directly use a method for that action.

As this is not quite clear without examples, maybe taking a look at the methods themselves can explain where these methods come in handy.


## List of These methods

> The syntax used to define meta methods in the examples provided below are not the real syntax. They are just for the demonstration.


### get

When user tries "instance`[item]`" this method will return the result. This is mostly used to add indexing option to the type.\
This method will be called with throwing `item` as the argument of it.

    func META:get(item) {
        ...
    }

But this is not the only way to implement it as it also works on slices. (using "instance`[1,5]`")

    func META:get(start, stop) {
        ...
    }

In fact this method can take as much arguments you want it to take. So for example if this method is implemented with 3 parameters then 3 items can be given in between of brackets.

> Default arguments can also be useful when implementing this method for different data types


### set

`set` is the exact opposite of get. It is used to set a value to a key (probably index). For example: `MyArray[2] = ...`

> `set` may also be implemented with multiple arguments

    func META:set(item) {
        ...
    }


### hash

To get the hash of the instance. When having 2 instances, hash is the proof they hold the same data or not which means if they hold different data they must return different hash and if they hold similar data then they have to have the same hash.\
All built-in data types must guarantee this statement but user defined classes may violate this (though it is not recommended).

> if the `meta:equals` is not implemented for a data type, the language will try `meta:hash` to check for equality and if this method is not implemented then it will raise an error

    func META:hash(item) {
        ...
    }


### includes

When trying to see if the instance contains something specific this method is used. Typically this method is implemented for collection types where they store multiple instances in them. Example `5 in MyArray` -> `true`

    func META:includes(item) -> Boolean {
        ...
    }


### iter

This method let the user use this instance in a for loop. Each round of for loop this method will be called. The return of this method will be set to the variable of for loop.\
For example in **`for item of MyInstance`**, the `meta:iter` of _`MyInstance`_ is called and _`item`_ will hold return of it during the round.

    func META:iter(previous_id) {
        ...
    }

> Read more about for loops and how they work [here](/docs/Principals/control_flow/for_loop.md)



### call

If the object can be called (just like a function), the `meta:call` must be used. `meta:call` makes the instance exactly like a function with providing the instance, ability to be called, take arguments, having defaults and return.

    func META:call(...) {
        ...
    }


### copy

In several cases the copy of the object is needed and it costs a lot of time by default.\
With implementing `meta:copy` the copy action on the data type objects can be customized and also optimized.\
Read more about copying in the docs!

    func META:copy(){
        ...
    }


### constructor

Probably the most important meta method is `constructor`. The constructor will initialize the instance. All attributes needed for the instance to be created can be implemented by constructors. Also methods can be called through the initialization. This method can also handle the object creation.

> Constructors will return the instance they are creating, but if the user returns something in the constructor, it will be the value your object will hold.

    func META:constructor() {
        ...
    }


### destructor

Unlike constructor which is the most used meta method, the destructor is one of the least used meta methods.\
This method handles what should happen when deleting the instance. The important part of this method that must not be forgotten is that it will be called before the language handle the deletion of it from the _`objects mapping`_ \

> destructors are mostly used for cleanups that need to be done outside of the instance.

    func META:destructor() {
        ...
    }
