# Factories Mapping

Beside having 2 mappings for objects and variables, there's another mapping for factories called `Factories Mapping` with a structure defined below.

    Name = Mapping:
                "type" = type
                "data" = Mapping : ...
                                   // This varies for each of the factories

No variables are allowed to be created with a name that exists in this mapping. If a variable has already been created with a name and then a class/function/module with the same name is declared, error will be raised.

> Since each of the factories have their own structure in FM, all of them are included in the list below


## Functions

    {
        "type": "function",
        "data": {
            "tasks": TaskObject_structure  // read more about `Task` in it's own doc
            "container": {
                "ATTR_NAME": VALUE
            }
        }
    },


## Methods

    {
        "type": "function",
        "access_identifier":  "public" or "private",
        "data": {
            "tasks": TaskObject_structure  // read more about `Task` in it's own doc
            "container": {
                "ATTR_NAME": VALUE
            }
        }
    },


## Classes

    "CLASS_NAME": {
        "type": "class",
        "data": {
            "parents": ["BaseClass"],
            "methods": {
                "instance": {
                    "method1": FMV_structure,  // with type of `method`
                    "method2": FMV_structure,  // with type of `method`
                },
                "class": {
                    "classmethod1": FMV_structure  // with type of `method`
                },
                "meta": {},
                "casting": {},
                "operator": {}
            }
        }
    },


## Structs

    "STRUCT_NAME": {
        "type": "struct",
        "data": {
            "attributes": {
                "attr1": type_name,  // value is a key of FM (or so called FMK)
                "attr2": type_name,  // value is a key of FM (or so called FMK)
            }
        }
    },


## Enums

    "ENUM_NAME" : {
        "type" : "enum",
        "data" : {
            "attributes" : {
                "ATTR1": null,      // user can optionally set a value to these attributes
                "ATTR2": null,    //  if a value is not set, it will be default to the attribute name
                "ATTR3": null
            },
            "methods": {
                "instance": {
                    "method1": FMV_structure,  // with type of `method`
                    "method2": FMV_structure,  // with type of `method`
                },
                "class": {}
            }
        }
    },
