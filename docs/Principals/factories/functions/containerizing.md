# Containerizing

Function (and also methods), beside their primary goal, can act like a key-value pair data structure.

You can set attributes to functions and access those attribute using the function and attribute name.
This is called Containerzing a function.

```shifty
func f(x):
    return f.y + x

f.y = 5
stdout(f(10))  // prints out `15`
```


Containerizing a function can be useful in several cases:

- Saving previous results (like _caching_)
- Permanently changing behaviour of the function from outside (not necessarily permanently, but at least for several calls)
- Having a behavioural data holder


Things to note about containerzing a function:

- Function containerizing is less secure than using arguments\
    When using function container, the behaviour of the function is not explicit in calls.
- Can cause conflict with `Single Responsibility` principle
