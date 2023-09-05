# Objects: Constants

Constants are a kind of variable/objects that will not change after their declaration.
As you saw in the `objects mapping`, there is a key called `const` which indicates whether the data of the object can be changed or not.
Now how does this protect variables if we redeclare one? Well, when trying to declare a variable, first thing that is checked is that if a variable with the same name is defined or not. if defined, then the object it holds is checked to see if it is a constant variable or not. if it's a constant, then `ConstantModificationError` will be raised.

Though this protects the variable, still the object `data` is not protected.\
This is handled when trying to initialize a variable as a constant. All attributes it holds will set as constant in their objects, which will block any attempts to change the objects defined in the base object.

Problem with constants comes with using them together with references.\
If an attribute of a constant is a reference to another object, this means that attribute will not be set as constant and it might change later on. Although this should not raise error since references are always used explicitly, but this should show a warning to the user as the constant variable/object is not really constant (due to the use of this reference). If the given reference object is a constant by it self, no changes can be done in the new object hence no warning will be shown.

    // e.g 1:
    const a = Person(firstname="Peter", lastname="Griffin")
    a.lastname = "Parker"   // this will raise error as the data is being changed
    a = 5   // this will also raise error as the constant variable is being redefined

    // e.g 2:
    name = "Peter"
    const a = Person(firstname=&name, lastname="Griffin")  // This should give user a warning as firstname is free to change.
    name += "..."  // now a.firstname is also "Peter..." since it is not constant
