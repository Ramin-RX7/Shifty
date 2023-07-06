# Builtins: functions:

The functions listed below are the ones implemented by language itself in order to remove duplicate code in different (independent) libraries. Also these functions may have access to some parts of the language that are not visible by the user (e.g memory location of objects, private attributes, etc.).



## apply

    func apply(f:Callable, object:Iterable) -> tuple;

This will call the function `f` on each element stored in `object`. Returns a tuple of each call result.

<br>

## filter

    func filter(f:Callable, object:Iterable) -> tuple;

Calls `f` for each element in `object`, if return is a truthy value, the element will be added to the returning tuple.

<br>

## all_of

    func all_of(object:Iterable) -> bool;

Returns `true` if all of the elements in an iterable are truthy values. (One falsy value is enough for `false` return)

<br>

## some_of

    func some_of(object:Iterable) -> bool;

Returns true if at least one of the elements in an iterable is a truthy value. Returns `false` if none of the elements are truthy.

<br>

## none_of

    func none_of(object:Iterable) -> bool;

Returns `true` if none of elements in an iterable are truthy values. (One truthy value result in `false`)

<br>

### hash

    func hash(object);

Returns hash of the given object. (Object must have implemented the `Meta-hash` method)

<br>

### input

    func input(prompt:Displayable) -> String;

Prompts for the user input. reads a line and return it as String.

<br>

### issubclass

    func issubclass(class_:type, parent_class:type) -> bool;

Determines wether the `class_` is a subclass of `parent_class`

<br>

### is_of

    func is_of(class_, classes:Union) -> bool;

Detemines wether a class is in the list of classes a Union holds

<br>

### type

    func type(object) -> Type;

Returns the class of the object.

<br>

### print

    func print(object:Displayable) -> null;

prints given object to stdout.
