# Operator Methods

As mentioned in `Special-Methods`, operator method are one type of them which control how different operators must behave with different types.\
Operator methods (binary) are called when an operator is used after an instance of the class.
If the class has defined the method for the corresponding operator, it will be called.
By default `operator-methods` return type is the class they are defined in. Which means if the return type is dropped in the syntax, the method must return an instance of the same class.

As operators are defined for the instance on the left side of the operator, each of these methods will have one (and only one) parameter that will stand for the instance on the right side. Type of the parameter defines whether the operation used in the users code is valid or not.

* If operation is not defined in the class of the left side instance, the same operation will be called for the instance on the right side (if exists) (with giving the left side instance as the argument).
* If it fails because of using a wrong type on the right side of the operator (comparing to defined parameter in method), the corresponding method from the right side of the operator will be called (if exists) only if it has the same return type as the left side method.

<br>

## Example

We can use `==` operator to check if two objects hold the same value or not

    func OP:==(other_object:String) -> Boolean {
        ...
    }

This means that this class can now be used in `==` operation.

Here's the list of operators:

- Comparison: `==`, `!=`, `>`, `>=`, `<`, `<=`
- Mathematical: `+`, `-`, `*`, `/`, `%`, `//`
- Logical: `^`, `||`, `&&`
- Unary: `~`


> (Waiting for decision) these method must have a fixed name parameter for the right side (So the method body is more understandable in all codes).

> (Waiting for decision) Since these methods should not have any side effect to the object, the object must have the same state as it had before the operation. Different options in this situation:
> * Make a copy of object and set it as the `self` parameter
> * Make object constant for the method body
> * (Preferred) Set this as a language convention but not limit the users for any changes the object


