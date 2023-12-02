# acquiring the functions

Functions can be used as key-value pair containers too.

Just like methods of class where we have a `self` keyword, a function can be self-containerized with using `func` keyword.

You can set attributes to function simply with the syntax below:

```shifty
#acquire(func)
func my_func(){
    stdout(func.attr1)
}

my_func.attr1 = "myname"

my_func()  // prints out `myname`
```

in the first line where we use `#acquire(func)`, we are simply telling `Shifty` that in this function body, we can use the `func` keyword to access the container of itself. This action is called `acquiring the function`

> Suggestion for names instead of `acquire`: empower, permit, equip, supply,

> Note that this is not a feature, this is a shortcut to make refactoring the function names easier. See below:

in the `my_func` body, we try to access the `attr1` attribute of the function. This could also be achieved via `my_func.attr1` too so what's the point of this?



## Advantages

`func` keyword brings 2 advantages to the topic of containerizing the functions:

### Readability
  - When reading function body, we do not need to know the function name and `func` simply means the function we are currently in.
  - When reading the code, it implies that this function uses it's own container and is self-aware of it.

### Refactoring
  - When renaming the function, you don't need to change the function body
