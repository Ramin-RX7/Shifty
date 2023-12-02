# methods

Methods of a class are separated into two main categories:

1. Instance methods:  These methods can only be called from an instance of the class
2. Class methods:  These methods are associated with the class itself rather than instances (must be called from class name)


## Special methods

Special methods are related to instance behavior in more general purposes.
These methods implement extra bits to objects.

> They are documented in [SpecialMethods](/docs/principals/factories/classes/special_methods/special_methods.md)



## equiring the methods

Methods can be decorated with a `acquire` utility to be given permission on using data container of class, object and even the themselves.

The same thing that we have in the normal functions where we can use `func`, we can access to class with `cls` and access to instance with `self`.

By default, when not explicitly acquiring a method, it is set as `#acquire(self)` which means it's an instance method.

> When using `#acquire` explicitely, it will replace the default.


**Examples:**

```shifty
class MyClass {
    #acquire(self,cls,func)
    func my_method(){
        // here we have access to the cls, self, and func
    }
}
```

Although a method can have all three of `self`, `cls` and `func`, it is important to know when to use each of them.

When acquiring a method:
- giving it the `self` means it is an instance method.
- giving the `cls` means it can access the class related data
- giving the `func` means the container of it is called `func` inside it's body


when a method is acquired with `self`, it is considered an instance method and when `self` is not acquired, the method is considered a class method.

As said before, methods can only be an instance method or class method. When not acquire the `self` (which means it is a class method), it is required to acquire the method with `cls` (since a class method must have access to class data)
