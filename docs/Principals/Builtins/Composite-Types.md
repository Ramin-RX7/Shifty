# Builtins: Composite types

Built-in classes may have more control over their objects and can have their own structure of `objects mapping`.\
No method/attribute can be overwritten in builtin types. Even classes that inherit from them.


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



## List

Dynamic sized Iterable that can only hold one type as it's elements.

**Meta methods:**

    Constructor(object) -> List {...};
    Equals ->  "true" only if both lists contains same elements in the same order
    Copy   ->  A new list object of the same elements
    Iter   ->  Return each element of the list.
    Get    ->  Gets the element in the given index (indexes can only be Integers)
    Includes ->  Checks if an element is in the tuple

**Casting methods:**

    Iterable -> Sends each list element as argument to the constructor
    String -> The same way the tuple is can be implemented in the language



## Dictionary

(Waiting for decision) Must be implemented using two dynamic-sized arrays. One array for keys and one for values.
When user wants to get a value of a certain key, first the index of the key in the keys array must be get. Then the same element in `values array` will be returned to the user.

**Meta methods:**

    Constructor(object) -> List {...};
    Equals ->  "true" only if both dictionaries contains same key-value pairs (order is not important)
    Copy   ->  A new dictionary object of the same elements
    Iter   ->  Return tuple of key and value of the dict.
    Get    ->  Gets the value of given key
    Includes ->  Checks if an element is in the dictionary keys

**Casting methods:**
    String -> The same way the tuple is can be implemented in the language
