# Objects

Objects are the most important parts of every programming languages. The way they are stored, read, written is a crucial part since it is responsible for performance and security.

In this language, we will have two main mappings that control how our objects are stored and accessed: `Objects mapping` and `Variables mapping`.

> In the docs we will use `VM` as an abbreviation for `Variables mapping`. Same thing is also used for `Objects mapping` which is `OM`.

Let's use an example to see how they work together:

    // Users code:
    my_variable = MyClass()

When an object is created (in this example an instance of `MyClass`), it will have a unique id determined by the language set to it. This is then used in the OM to save the object.

    // Language creates a unique id
    // For example it will give us `#123`
    // This result like this in the OM:

    objects_mapping = {
        #123 : MY_CLASS_OBJ
    }

Now since this object is (probably) be assigned to a variable, in the VM we will have:

    variables_mapping = {
        my_variable : Ref(#123)
    }

This means when user tries to use the `my_variable` in their code, language will first search in the VM, finds the name and gets the value of it. Then Searches through the OM to find the key and gets the value it holds.


That was how OM and VM work in an example. Now their real structure:

    Objects mapping = {
        ID = Mapping:{
            "type"  =  type_name
            "data"  =  {     // data of the instance (based on type)
                "attributes" : {
                    name : OMV | Ref(id)
                }
            }
            "const" =  bool    // if the object/variable is a constant
            "reference_count" = int
        }
    }

    Variables Mapping = {
        variable_name : Ref(ID)
    }

> `Ref(...)` in the variables mapping is explained in the references and garbage collection system sections.


### Objects mapping values (OMV)

The objects mapping might have simple keys (IDs) but the values it hold are quite complicated. The values structure is used in some other parts of the code and so the `OMV structure` is the name we will give to the structure.

`OMV` is a mapping-like structure that holds all the data needed for an object.

List of key-value pairs in `OMV`:

#### type
The "type" is responsible to hold the type name that this object is (This type name is the key that exist in `Factories mapping` that will be explained later on in this doc).

#### data
This is the exact position where the object data is stored. As of now, only `attributes` takes place in this mapping.\
`attributes` will be another mapping that holds the attribute names as the key and a OMV as it's value. The reason is that the attribute will hold an object and that object must follow the convention used for any other object in the language.\
We can also have the value as a `Ref` object.

#### const
this key will declare whether this object is constant or not (read more about constants [here](//docs/Principals/Objects/Constants.md))

#### reference count
Number of references this object currently has.

> Suggestion for threading use: "owner"="main" (the thread that this object belongs to (at the moment))




## Declaring variable type

Variables must be initialized in their declaration time.\
Variables are not forced to explicitly define their type in declaration.\
function parameters must declare their type.\
function return type is neccessarily but can be dropped in syntax if no return is in the function.





# Todo/Notes of this doc:

Scopes implementation

Check marks-and-sweep algorithm for garbage collection system

Some algorithms to stop cyclic references when using marks-and-sweep: Cheney's algorithm, Baker's algorithm, and the "two-finger" algorithm

**Object Pooling System**:

- Using object-pooling and concurrent garbage collection system at the same time (hybrid grabage collector)
- Users be able to set a flag when making classes to indicate wether objects of this class should be pooled in object pooling system or not.
- ? Using a fixed size object pooling system or dynamic sized?
- ? Let the size of the pool be configurable by user?
