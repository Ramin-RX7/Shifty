# Dynamic Block

> This doc is not yet accepted. However it might be in the future.

Unlike expressions which must return an object, statements do not necessarily return something. However with changing some blocks that are considered statement in other languages to expressions, we can dynamically use many blocks within each other.

This means we can turn some blocks that do not return a value in other languages to expressions so we can retrieve data from them.

As an example loops, pattern-check, try-except blocks can return something.

Also creating functions, classes (and other factories) result in creating a factory dynamically.

Here is an example:

```shifty
func f(x){
    ...
}

i = 2
f(match (i){
    case (1){ "a" },
    case (2){ "b" },
    case (3){ "c" },
})
```

This will run the pattern-check. It returns `"b"`. `"b"` will be sent to `f` as `x` argument.



## Outcome

Nested expression and statements.

- Reduce the readability
- Blurrify the distinction of statements and expression
- Removes one-time-needed variables
- Allows dynamic factory generation
  - Removes lambda
