# Error Handling


## FailSafe operator (`?` operator)

This can be used after any expression to let the language know that this expression might raise an error and has to be caught by the language.\
If the expression executes normally, it will return the expected value. But if any error occurs during the compution of the expression, the instance of the error that is raised will be returned.

> Some other names that we can have for this operator: `Fallback`,`ErrAware`


