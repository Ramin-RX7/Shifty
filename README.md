# Shifty


## Brief explanation

`shifty` is a programming language which is still in it's early stages of development (very early).

As of now, the principles that builds up the main structure of the language are being worked on.

The concept are all explained in a high-level environment (since I'm personally not familiar with low-level concepts in creating a language). These concept can be easily understood with no need of deep knowledge in other languages.

In `shifty` we try to provide an easy to use interface for users with ability to validate any type of data received from foreign sources.

Since the start of this project my hope was to build it with Rust (due to security and performance), although this is not definite.



## Goals

- Easy data validation
- Providing a readable structure (even for low level parts of the language)
- Similar interface to work with different data types/formats
- Feature-rich error handling
- Concurrent execution
- Freedom limitations be set by user not language
- Include vast amount of generally needed operations in the standard library
- Easily interacting with the base language



## Features

We try to adapt any feature that can help getting closer to the main goals from other designs. These features may not necessarily come from other languages but can be drived from some software designs.

As an example multiple inheritance of `shifty` uses the same concept python uses called `MRO`.

However `shifty` also takes the `Atomic Transaction` concept from database atomicity (which is a property of ACID) and uses it in the error handling.



## Syntax

Although in principles you can see some examples with a custom syntax, the semantics for `shifty` is not tahiie yet. Albeit I want to have a syntax similar to the ones provided in the examples.

> Whenever syntax for `shifty` is defined, all the examples codes will be shipped to it.



## Contributing

Here in `Shify`, all contributions are welcome!

If you've found an issue in the docs or you have a feature request or even you have an idea, please open an issue and state whatever you have in your mind. We will be in touch to discuss whether the changes are useful and how must they be implemented together.

Also if you found a misspelled word or a grammatical problem, feel free to open a pull request (with no need of openning an issue.)



## License

`shifty` is licensed under `GNU General Public License v3.0`. Read more [here](/LICENSE)
