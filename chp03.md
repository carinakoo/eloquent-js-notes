# Functions

### Defining a function
* Functions are created with an expression beginning with keyword “function”
* Functions have parameters and a body. The body must be wrapped in braces.
* Functions may or may not produce a value
* If a return value is not specified, the function returns “undefined”

### Parameters and Scopes
* variables created inside a function are local to the function
* variables are re-created each time the function is called
* variables declared outside of any function are “global” variables

### Nested Scope
* functions can be created inside other functions
* lexical scoping: the scope depends on the position of the function in the code. the function scope can see its parent scopes. functions declared inside another function can access the outer function’s local scope.
* let: in ES6, let variables are local to the enclosing block, not the enclosing function

### Functions as Values
* function values can be used as expressions, stored in different variables, passed as arguments

### Declaration Notation
* function declaration begins with the keyword “function” as in “function square(x) { return x*x }”
* function declarations are hoisted to the top of their scope
* do not use function declarations in “if” blocks

### The Call Stack
* call stack: used by the program to store the context of execution
* When the call stack grows too big, computer fails “out of stack space” or “too much recursion”

### Optional Arguments
* When you pass too many arguments, extras are ignored
* When you pass too few arguments, missing parameters get the value “undefined”
* This allows arguments to be optional

### Closure
* closure: a function that “closes over” some local variables and is then able to reference specific instances of those variables
* when a function is returned as a value, it “freezes” the code in its body and wraps it into a package which is returned as the function value

### Recursion
* recursive: when a function calls itself
* can result in simpler code
* often slower than non-recursive versions of same functionality
* don’t optimize until you know it’s a problem
* some problems are much easier to solve with recursion, typically for example when needing to trace multiple exponentially expanding branches
* example: find solution to adding 5 and multiplying by 3 to reach an arbitrary number

### Growing Functions
* a couple typical cases that necessitate new functions to be written:
    * avoid repeating code multiple times
    * missing functionality
* a function name is indicative of how clear the concept is whose functionality you’re writing
* a useful principle: don’t add cleverness unless you’re sure you’re going to need it

### Functions and Side Effects
* pure functions: functions that produce a value without side effects, and does not rely on side effects from other code
* pure functions always produce the same value when given the same arguments
* pure functions are easier to reason about, since they are not affected by arbitrary variables outside of it
