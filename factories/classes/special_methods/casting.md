# Description

This group of methods includes the ones that handle how to cast instances of a class to another class.

When working with functions sometimes a call might comes with wrong argument types. Let's say we have `f(x)` where `x` must be of type `MyClass`. If we call `f` with an instance of `OtherClass` as `x` argument, we must get an error. But because `OtherClass` has implemented the casting method to `MyClass` instance, `x` argument we sent will be converted to `MyClass` and the program keeps working correctly.

# Rules

There are several rules when using these methods.

- A casting method has to return a value of the type it is being casted to. The return type is not overwritable.
- When the function parameter takes a reference, casting methods will not work (As the actual object is not sent to the function)

# Methods related to casting

When a class defines a casting method for another type, the language will collect this method and save it so later on knows which types this class can be casted to. 

> [!attention] TLDR
> This is somehow a cache type of thing, which means if there are many classes defined (with operator method definitions) can cause start-up issues

## `cast` methods

The action of implicit casting uses the `cast()` method to convert types.
This method takes required argument of type which is the type it is going to cast the instance.

```
class MyClass {
    ...
    {cast}OtherClass(){
        // Code in this block will be executed when an object of 
        // this class (MyClass) is being converted to `OtherClass`
        // some code that return an object of OtherClass in the end
    }
    ...
}
func f(x:OtherClass){
    ...
}

a = MyClass()
func(a)          // here the implicit casting happens

```

In the above example, since `a` has the type of `MyClass` but function takes an instance of `OtherClass`, language tries to cast `a` to `OtherClass`. Because the `MyClass` defines a casting method for `OtherClass` this is possible. The way it is handled by the language is using `.cast(OtherClass)` method.

> [!attention]
> There must be a way to validate the return type of the method and definition of the method.
> Method name must be same as the Type it is returning 

User can use this method to explicitly cast to other types.

The difference between implicit and explicit casting is the error they raise when they can not find the needed method.
In explicit, user will face `NotImplementedCasting` error but in implicit, `ImplicitCasting` error.
Since both of these errors are derived from `CastingError` , they can be caught separately and/or together.

> (Waiting for decision) Another name for this method can be `as`

## `from` method

Also there is another final method in `Type` named `from`. `from` is a class method which is opposite of `cast()`.

The reason behind having this method is to be able to extend built-in classes (such as String, Float, etc.) without needing to override them. Suppose a type wants to let user convert another type to it. This will be helpful


```
class Json {
    {from} Array() {
        ...
    }
}
```

Example above shows a way to extend the `Array` built-in class and let them be able to convert to `Json` type user is defining.

> [!note]
> Since scopes makes it clear that we can define `cast` method for classes that are previously defined in the current scope.
> also `from` can only be defined for previous classes which means no priority will be considered as only one of them can be done! 