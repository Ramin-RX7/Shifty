# For loop

`for` loops can be run over any type instance that implements `META:iter`.

Before knowing how `for` loop works, we need to know how to implement a proper `META:iter` method.

The syntax provided for it is:

    func META:iter(previous_id=null) {
        ...
    }



`iter` method takes an argument which determines what must be generated in the next iteration. On every call, it needs to return a tuple of:
1. unique identifier for the current iteration
2. the object returned by the current iteration

> The identifier returned by the `iter` implies that a specific result has been generated and in the next iteration it will be used to find what must be returned this round.


So let's start figuring out how exactly do for loops use `META:iter` !

At the start, loop will call the `iter` method. Since no iteration has been done yet, no argument will be given in this call. Now iter must return a tuple of `(UNIQUE_ID, INIT_OBJECT)`. Then the loop body will be executed until we reach the end of it and we have to run the next iteration.\
Once again the loop calls the `iter` method but this time with giving the `UNIQUE_ID` as the argument. In the `iter` body, the logic of how this identifier will be used to generate next item is defined.

Let's see this in an example

    class MyClass {
        func META:constructor(){
            self.letters = ["a", "b", "c"]
        }

        func META:iter(previous_id=-1){
            new_identifier = previous_id+1
            return (new_identifier, self.letters[new_identifier])
        }
    }

    for letter of MyClass() {
        stdout(letter)
    }

In this example we have a class which wants to implement the iteration logic over the `letters` attribute of itself.

When encountering the for loop, `iter` will be called with giving no argument. So the default value (`-1`) will be used. Then in the body, it will get the `-1`, runs the new item identifier logic (`new_identifier = previous_id+1`) and then returns the new identifier and the object we need to use. The first item of the returned tuple will be saved in the loop memory and the second item will be set as `letter` value. In the body of the loop we print the letter to the standard output and this round is completed.

Now in the next round, the loop will call iter with the identifer it recerived from the last call (which was `0`). Again the logic of the iteration will be executed and so we go to the next round.

This however has a slightly big issue. In the fourth round we will encounter the `IndexError` since the `self.letters[new_identifier]` will tries to get an element out of the `letters` array bound. So what to do in these situation?

For loops will be executed eternally until an `EndOfIteration` error is raised within the `iter` call. So we can define a logic in the `iter` to raise this error when the for loop needs to end. Let's rewrite the example with handling the error we mentioned.

    ...

        func META:iter(previous_id=-1){
            new_identifier = previous_id+1
            if (new_identifier >= self.letters.size) {
                throw EndOfIteration
            }
            return (new_identifier, self.letters[new_identifier])
        }

    ...

This is a good solution that will block the loop execution after reaching the maximum letters list length.



## Advantages/Disadvantages

- This way if a specific offset want to be given for the iteration it is possible.

- It makes it harder to implement `META:Iter` for types since they're complicated; Using `yield` can help a lot for this situation
