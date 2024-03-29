# Builtins: Composite types

Composite types consist of types that are a bit more complex than Primitive types. Mostly the types defined here are collection types which means they are a data type that can hold multiple of instances of other types.


## Tuple

Fixed size Iterable that can hold multiple types in it.

**Meta methods:**

    Constructor(object) -> Tuple {...};
    Equals ->  "true" only if both tuples contains same elements in the same order
    Copy   ->  A new tuple object of the same elements
    Iter   ->  Return each element of the tuple.
    Get    ->  Gets the element in the given index (indexes can only be Integers)
    Includes ->  Checks if an element is in the tuple

**Casting methods:**

    Iterable -> Sends each element as argument to the constructor
    String -> The same way the tuple is can be implemented in the language



## Array

Dynamic sized Iterable that can only hold one type as it's elements.

**Meta methods:**

    Constructor(object) -> Array {...};
    Equals ->  "true" only if both arrays contains same elements in the same order
    Copy   ->  A new array object of the same elements
    Iter   ->  Return each element of the array.
    Get    ->  Gets the element in the given index (indexes can only be Integers)
    Includes ->  Checks if an element is in the tuple

**Casting methods:**

    Iterable -> Sends each array element as argument to the constructor
    String -> The same way the tuple is can be implemented in the language



## Mapping

(Waiting for decision) Must be implemented using two dynamic-sized arrays. One array for keys and one for values.
When user wants to get a value of a certain key, first the index of the key in the keys array must be get. Then the same element in `values array` will be returned to the user.

**Meta methods:**

    Constructor(object) -> Mapping {...};
    Equals ->  "true" only if both mappings contains same key-value pairs (order is not important)
    Copy   ->  A new mapping object of the same elements
    Iter   ->  Return tuple of key and value of the mappings.
    Get    ->  Gets the value of given key
    Includes ->  Checks if an element is in the mapping keys

**Casting methods:**
    String -> The same way the tuple is can be implemented in the language
