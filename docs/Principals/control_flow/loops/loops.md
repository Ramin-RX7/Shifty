# Loops

> (Waiting for decision) Although the whole section below looks alright but still it is related to dynamic object creation concept where all statements must return something

Loops works the same as other languages with addition of returning completion method and an object.

Loops will return two values:
1. `completed`: A boolean showing how the loop has ended
2. `value`: What did the loop give out

Whenever a loop is ended, either the loop has decided to end itself, or we have reached a user `break` keyword.

if the loop completely finishes, we will set `completed` to `true` but if we reach a `break`, `completed` will be `false`.

When reaching a `break`, an object can be put in front of it which will be set as the `value`


```shifty
// No `break`
i = 0
completed,result = while (i<6){
    stdout(i)
    i = i+1
}
stdout(completed)   // true, since the loop has ended all of it's iterations succesfully
stdout(result)      // null, since we haven't reached a break


# plain `break`
i = 0
completed,result = while (i<6){
    stdout(i)
    i = i+1
    if (i==4){
        break
    }
}
stdout(completed)   // false, since `break` has ended the execution
stdout(result)      // null, since we haven't reached a break with an object in front of it


# `break` with object
i = 0
completed,result = while (i<6){
    stdout(i)
    i = i+1
    if (i==4){
        break "result"
    }
}
stdout(completed)   // false, since `break` has ended the execution
stdout(result)      // "result"
```
