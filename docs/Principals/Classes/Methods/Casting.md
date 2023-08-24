# Classes: Methods: Casting methods


This group of methods includes the ones that handle how to cast instances of a class to another class.\

When working with functions sometimes may a call comes with wrong argument types. Let's say we have `f(x)` where `x` must be of type `MyClass`. If we call `f` with an instance of `OtherClass` as `x` argument, we must get an error. But because `OtherClass` has implemented the casting method to `MyClass` instance, `x` argument we sent will be converted to `MyClass` and the program keeps working correctly.


There are several rules when using these methods.

- A casting method has to return a value of the type it is being casted to. The return type is not overwritable.
- When the function parameter takes a reference, casting methods will not work (As the actual object is not sent to the function)


## Methods related to casting

When a class defines a casting method for another type, the language will collect this method and save it so later on knows which types this class can be casted to. The action of implicit casting uses the `as()` method to convert types.\
This method takes required argument of type which is the type it is going to cast the instance.

    class MyClass {
        ...
        {cast}OtherClass(){
            // Code in this block will be executed when an object of this class (MyClass) is being converted to `OtherClass`
            // some code that return an object of OtherClass in the end
        }
        ...
    }
    func f(x:OtherClass){
        ...
    }

    a = MyClass()
    func(a)          // here the implicit casting happens

In the above example, since `a` has the type of MyClass but function takes an instance of `OtherClass`, language tries to cast `a` to `OtherClass`. Because the `MyClass` defines a casting method for `OtherClass` this is possible. The way it is handled by the language is using `.as(OtherClass)` method.

`.as(type)` is a finalized method on `Type` class which is used to convert types.

User can use this method to explicitly cast to other types.

The difference between implicit and explicit casting is the error they raise when they can not find the needed method.\
In explicit, user will face `NotImplementedCasting` error but in implicit, `ImplicitCasting` error.\
Since both of these errors derive from `Casting` error, they can be caught separately and/or together



> (Waiting for decision) Access the casting methods directly. This makes the code much better when argument is needed in casting.


> Note: the section below is not yet approved (Waiting for decision).

Also there is another final method in `Type` named `from`. `from` is a class method which is opposite of `as()`.\

    // using previous example functions and classes
    a_as_otherClass = OtherClass.from(a)
    // this is the same as using the code below
    a_as_otherClass = a.as(OtherClass)

Now since the use of `from` method looks the same as `as` method, there are few notes worth mentioning:
???
