# Objects: References


## Prerequisite

Before getting into references, it's better to have a good understanding of VM and OM.

Let's say both "a" and "b" are variables pointing to the same object.\
When "a" changes something in it's object, because "b" refers to the same object, the value of "b" also changes.\

Demonstration in the code:
    // Mappings:
    objects_mapping = {
        #123 : ...  // let's say it holds and integer of "5"
    }

    variables_mapping = {
        "a" : Ref(#123),
        "b" : Ref(#123),
    }


    // User Code:
    a += 1

Steps of the above operation:
1. Search for `a` in the VM
2. Get the id it holds.
3. Find the id in the OM
4. Apply the operation (increase by 1)

Since the data is changed in the **_object_**, now `b` also has the value of `6`.


Now that the required explanations are given, we can talk about `references`.


## References

Refrences are a way of getting the object a variable is pointing to.
When setting reference of a variable as another variables value, basically what happens is that the `id` of the former will be set as the `id` of the defining variable. So any changes to either of them (changes in object) will also affect the other one.

(*This differs from c++ references in some aspects.*)

    // Example:
    a = 5
    b = &a     // suppose `&` makes a reference of variable in our language
    b += 1     // as both `a` and `b` points to same object, now both of them are equal to 6

> the line `b = &a` will find the id of the object that `a` is holding and set it to `b`.


Different use of this:

- When sending them as a function argument, the actual object will be sent. (read more [here](/docs/principals/Functions.md/#parameters))\
- When trying to set a new value to a variable but still need previous.\
- When we want to make an alias for a variable

The most important one is the function calls. In a normal function call, the objects are copied and then sent to the function. Using references we can send the actual object which will improve the performance a lot.

