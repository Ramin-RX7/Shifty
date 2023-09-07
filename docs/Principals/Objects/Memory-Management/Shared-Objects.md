# Objects: Memory-Management: Shared-Objects


A key part of a programming language is how it handles memory. Here we use reference counting as the base of our memory management to make sure objects only exist if they are needed. Although the main memory management method is reference counting, but we also use ownership rules to decrease the complexity and ease of handling objects.

When an object is created, it will be saved to OM. This is not quite right about objects within other objects.

As mentioned in the docs, in the OM objects, we will include some other objects like `attributes`. In the `attributes` mapping we have OMV structure again. This is because we will save the data of a specific object inside itself. When that object is deleted, any children it had will be deleted too (just like Cascade deleting in SQL). The reason is those objects are not used by other objects.\
Mostly when using objects within other objects, they will have one owner which is their parent. But sometimes an object within an object is referenced in a totally sparate object.

    a = MyClass(name="Peter", age=25)

    b = MyClass()
    b.name = &(a.name)

Here we try to use the `a.name` object for `b.name`, this will work well unless the `a` is deleted (for any reason). When `a` gets deleted, all the childrens of it will be deleted too. This means the corresponding object for `a.name` will be deleted. Now what happens to `b.name`? Now we have a variable with dangling reference.
To avoid situations like this, when a reference to an inner object is requested, we will take it out of it's parent scope and move it to the OM. Now we will fill the place it used to be with the id of it in the OM. Since the object is now easily accessible throughout the program, we can assign the new variable id to the new id we made.

Here are the OM and VM before and after the `b.name = &(a.name)` line:


    objects_mapping = {
        "123" : {
            "type" : "MyClass",
            "data" : {
                "attribute" : {
                    "name" : {
                        "type" : "string",
                        "data" : {   // Builtin types have their own schema for `data` key values
                            value : "Peter"
                        },
                        "const" : false,
                        "reference_count" : 1,
                    },
                    "age" : {
                        ...  // does not matter for the sake of example
                    }
                }
            },
            "const" : false,
            "reference_count" : 1
        },

        "789" : {
            "type" : "MyClass",
            "data" : {
                "attribute" : {
                }
            },
            "const" : false,
            "reference_count" : 1
        }
    }

    variables_mapping = {
        "a" : Ref("123"),
        "b" : Ref("789"),
    }


Now the line is being executed an the `a.name` has to be taken out from the object data to the OM:

    objects_mapping = {
        "123" : {
            "type" : "MyClass",
            "data" : {
                "attribute" : {
                    "name" : Ref("xyz")
                    "age" : {
                        ...  // does not change
                    }
                }
            },
            "const" : false,
            "reference_count" : 1
        },

        "789" : {
            "type" : "MyClass",
            "data" : {
                "attribute" : {
                    "name" : Ref("xyz")
                }
            },
            "const" : false,
            "reference_count" : 1
        },

        "xyz" : {
            "type" : "string",
            "data" : {
                value = "Peter"
            },
            "const" : false,
            "reference_count" : 2
        },
    }


As you can see, a new object is created in the OM (with id of `xyz`). Both of `a.name` and `b.name` now reference to this object. With this method, `xyz` is not dependent to `a`. if `a` will be deleted, it will only decrease the `reference_count` of `xyz`.
