# function iterators

Function iterators are special type of functions that work the same as generators in other programming languages.

> The logic behind having function iterators beside normal iterators (build with `META:iter`) is that some iterators might be type independent.


## what, why, how

These special types of functions can pause themselves, return a value, then again resume when user request them.

Let's see how they exactly they work with a useful example:

we have a array of numbers and we want to get the even numbers

first way to do this is:

```shifty
numbers = [1,4,5,2,6]

for (number of numbers){
    if (number%2 == 0){
        stdout(number)
    }
}
```

This works perfectly fine but what if we want to do the same thing over and over again in our application? In a situation like this we create a function that do this for us:

```shifty
func get_evens(numbers){
    even_numbers = []
    for (number of numbers){
        if (number%2 == 0){
            even_numbers.push(number)
        }
    }
    return even_number
}

numbers = [1,4,5,2,6]
for (number of get_evens(numbers)){
    stdout(number)
}
```

Now not only we moved the condition/logic to somewhere out of loop body but also made a reusable code. However this is not really memory and time efficient when dealing with massive data sizes and computations. Now `function iterators` come in handy.

function iterators help to save up more memory and also split the time consumption of each item generation to the moment that item is requested (lazy generation).

The correct way of solving the previous problem is `function iterator`. Take a look at the code below:

```shifty
func get_evens(numbers){
    for (number of numbers){
        if (number%2 == 0){
            yield number
        }
    }
}

numbers = [1,4,5,2,6]
for (number of get_evens(numbers)){
    stdout(number)
}
```

There's not much changes to the `get_evens` function, right? Although it's not really a big change in the code, a lot of different things will happen in the background.

> How does this save up memory?
>> we don't need to have a list that stores all even numbers to return them when they are all obtained
>
> How does this help performance?
>> When each new item is generated, we will give it out to the caller without waiting for anything else, hence each item will only takes time as much as it needs for itself.



## what happens behind the scenes

When this function is being parsed, in fact it is not going to be looked as a normal function in Shifty! When parsing the code, the `get_evens` is considered a `function iterator` which acts totally different.

> `function iterators` are specific type of function that use `InterruptibleTask` objects

> Before you see how this exactly works it's better to check how [for loops](/docs/principals/control_flow/for_loop.md) actually work.

in the first line of for loop (`for (number of get_evens(numbers))`), the loop will call `META:iter` of the `get_evens(numbers)`. Since calling the `get_evens(numbers)`, an object will be created that implements it.

This means the function will start executing until it reaches a `yield` statement. Now it's time to save all data of the function for now, pause the execution (for later resume), and return the value infront of `yield`.

Once again in the next round of loop, it will call the `META:iter` once again, Now the `InterruptibleTask` will reload everything it saved from previous call, and continue execution of the function. And this will run until we reach the end of the function body. Here the language will raise a `EndOfIteration` to inform the loop that the iteration is complete we can move on to the next code blocks.
