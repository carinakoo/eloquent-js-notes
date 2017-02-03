# Higher-Order Functions
### Intro
* Programs that break functionality down into conceptually meaningful pieces are more likely to be correct

### Abstraction
* *abstractions*: programming vocabulary that hides details and gives us the ability to talk about problems at a higher level
* A programming must acquire by second nature the ability to notice when a concept is ready to be abstracted

### Abstracting array traversal
* *forEach*: built-in array method abstracts the typical for loop array traversal by handling the traversal and hiding the details of the traversal implementation

### Higher-order functions
* *higher-order functions*: functions that operate on other functions, either by taking them as arguments or returning them
* functions can create new functions
* functions can change other functions
* functions can provide new types of control flow (e.g. unless, repeat)
* inner functions benefit from lexical scoping -- they have access to the variables defined in the outer function's scope

### Passing along arguments
* When modifying a function, how can you pass along an arbitrary number of arguments taken by the original function?
* Use the built-in function *apply* method to pass the original function's *arguments* object to the modified function (e.g. return f.apply(null, arguments))

### JSON
* JSON: JavaScript Object Notation widely used as a data storage and communication format on the web
* similar to JavaScript's format for arrays and objects, with added restrictions:
	* property names must be surrounded by double quotes
	* simple data only -- no functions or variables
	* no comments
* JSON.stringify and JSON.parse convert between JS values and JSON strings

### Filtering an array
* *filter* is a built-in method on arrays that creates a new array of elements which pass a given test

### Transforming with map
* *map* a built-in method on arrays that transforms an array by applying a function to all of its elements and building a new array from the returned values

### Summarizing with reduce
* *reduce* a built-in method on arrays that reduces all the elements of an array to one value, using the given "combine" function, which is applied to each array element to accumulate a result.

### Composability
* Higher-order functions are good for composing functions -- combining multiple functions representing different concepts

### The cost
* Re-creating arrays and multiple function calls have a performance cost, but fortunately for most applications this performance cost is irrelevant. The exceptions would be large datasets or events that happen with extreme frequency (not on a human timescale).

### Great-great-great-great-...
* Example higher-order functions for traversing and reducing a family tree

### Binding
* *bind* is a built-in method on functions which creates a new function that calls the original function with some of the arguments already fixed.
* the bound function is thus "partially applied"
* The first argument it takes is reserved for an object on which the function would act as an object method.

