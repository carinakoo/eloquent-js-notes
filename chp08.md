# Bugs and Error Handling

### Intro
* A program is crystallized thought
* Bugs can be programmer errors or problems in other systems that the program interacts with
* Bugs may be immediately apparent or remain hidden for years
* Problems can surface when a program encounters a situation that the programmer didn't originally consider

### Programmer mistakes
* Mistakes can range from simple typos to subtle mistakes in understanding the way the program operates
* Languages vary in how much they help find bugs
* JavaScript is not very helpful -- it's very flexible in what kind of statements it allows without complaining
* Things that JS will complain about:
	* invalid syntax
	* calling a non-function
	* looking up a property or undefined value
* *debugging*: the process of finding mistakes in programs

### Strict mode
* enabled by putting `"use strict"` at the top of a file or function body
* variables may not be used before declaring them
* `this` is undefined in functions that are not called as methods


    function NormalFunction() {
       console.log(typeof this); // object
    }

    function StrictFunction() {
      "use strict";
      console.log(typeof this); // undefined
    }

* invalidates multiple function parameters with the same name
* removes some problematic language features

### Testing
* Tests run a program and check that it does the right thing
* *test suite*: a collection of tests
* *testing frameworks*:software for testing that provides a language for expressing tests and outputting results

### Debugging
* Instead of making random changes to the code,
  * analyze and come up with a theory of what is happening
  * then make observations to test the theory
* use console.log to help observe behavior
* use browser debugger by setting breakpoints which allow you to step through code and inspect variable values

### Error propagation
* For errors that arise from user input or other external source, the program must either ignore the error, or surface the error in some way
* One option is to return a special null value, however this can lead to code cluttered with null checks

### Exceptions
* *exception handling*: exceptions make it possible for code that runs into a problem to *raise* or *throw* an exception
* an exception is simply a value
* *unwinding the stack*: when an exception is raised, it exits all its calling functions
* you can set "obstacles" along the stack to *catch* the exception as it exits
* `throw` keyword raises exception
* `catch` block is evaluated when `try` block raises exception
* `Exception` constructor creates object with
  * `message` property
  * (in modern environments) a `stack` property with info about the call stack at the time of exception called the *stack trace*
* Exceptions allow error handling code to be limited to 2 points:
  1. where the error occurs, and
  2. where the error is handled

### Cleaning up after exceptions
* `finally`: in a `try` statement, a `finally` block allows you to specify code that will run after the `try` block, whether or not an exception is caught
* the `finally` block is called even if the `try` block returns

### Selective catching
* When an exception makes it all the way to the bottom of the stack without being caught, it gets handled by the environment
* Invalid uses of the language will raise exceptions which will also be caught by any try statement in the stack
* To distinguish between the exception you are targeting and other exceptions:
  * Use a new error constructor which inherits from the built-in Error type.
  * Check the type of the exception using `instanceof`

### Assertions
* *assertions*: a compact way to enforce expectations, blowing up the program if the stated condition does not hold
* make sure that mistakes cause failures at the point of the mistake rather than silently producing nonsense values that may create further problems
