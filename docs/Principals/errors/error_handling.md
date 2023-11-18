# Error Handling


## FailSafe operator (`?` operator)

This can be used after any expression to let the language know that this expression might raise an error and has to be caught by the language.\
If the expression executes normally, it will return the expected value. But if any error occurs during the compution of the expression, the instance of the error that is raised will be returned.

> Some other names that we can have for this operator: `Fallback`,`ErrAware`



## Atomic blocks

These code blocks function similarly to atomic transactions often seen in databases. Within an AtomicBlock, you can group together a series of operations that modify the program's state or perform other tasks. The critical aspect is that these operations are treated as a single cohesive unit.

If any operation within the AtomicBlock encounters an issue and fails, all changes made by the entire block are automatically rolled back. This means that your program's state remains unchanged, and no partial modifications take effect.

By using AtomicBlocks, you can ensure that a set of operations is executed as an all-or-nothing proposition. This is particularly useful in scenarios where maintaining data consistency and reliability is paramount.

Additionally, you have the option to include a `catch` block following an `AtomicBlock`. This `catch` block can be used to catch and handle any errors that may have been raised within the `AtomicBlock`. However, using a `catch` block is not required, and if omitted, any errors will propagate as usual.


> Another name suggestion: `SafeTry`
