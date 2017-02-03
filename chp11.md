# Chapter 11: Project: A Programming Language
* We create our own programming language called Egg

### Parsing
* Syntax features of Egg
  * Everything is an expression
  * *expression*: variable, number, string, or application
  * *string*: a sequence of characters that are not double quotes, surrounded by double quotes
  * *number*: a sequence of digits
  * *variable names*: non-whitespace characters that have no special meaning in the Egg syntax
* A *syntax tree* data structure is used to describe a program written in Egg
  * consists of expression objects with `type` property indicating the kind of expression
    * `value` type: literal strings or numbers
    * `word` type: identifiers, with `name` property
    * `apply` type: applications, with `operator` and `args` properties
  * Example: >(x, 5)

        {
          type: "apply",
          operator: {type: "word", name: ">"},
          args: [
            {type: "word", name: "x"},
            {type: "value", value: 5}
          ]
        }

* `parseExpression` function:
  * takes a string input
  * returns object containing:
    1. data structure for the first expression in the string
    2. rest of the string
* `parseApply`:
  * if rest of string is application expression, creates data structure for expression
  * calls `parseExpression` recursively for each argument expression to process the complete string

### The evaluator
* runs the program given a program syntax tree
* retrieves values for each expression type
  * values are immediately returned from the expression objects
  * words are looked up in the environment
  * for applications, special forms are handled by another function, and regular applications are applied with their recursively evaluated argument expressions

### Special forms
* Special forms are part of Egg syntax
* `if` is a special form that takes 3 arguments, and is similar to JS ternary operator
* `while` takes 2 arguments, and calls evaluate on the 2nd argument while the 1st argument is not `false`
* `do` executes all its arguments from top to bottom
* `define` takes a word as its first argument and expression as its second argument and assigns the evaluated value of the expression to the word

### The environment
* The environment is an object where
  * properties whose names correspond to variable names
  * values correspond to the values the variables are bound to
* Boolean values are assigned to their string variable names


    var topEnv = Object.create(null);

    topEnv["true"] = true;
    topEnv["false"] = false;
* Arithmetic operators are defined in the environment as application expressions:

```
["+", "-", "*", "/", "==", "<", ">"].forEach(function(op) {
  topEnv[op] = new Function("a, b", "return a " + op + " b;");
});
```

* a `run` function takes a list of Egg expressions, joins them into one program string, and evaluates the string

### Functions
* A special form `fun` represents a function.
  * takes a list of arguments, the last of which is considered the function body
  * functions have their own local environment object created with the outer environment as its prototype

### Compilation
* *Compilation* is an optional step between parsing and running a program which transforms the program into a second form that can be evaluated more efficiently
* Traditionally involves converting the program to machine code

### Cheating
* The implementation of Egg on top of JavaScript may seem trivial or like cheating, as opposed to implementing a new language entirely in machine code
* However it can be more effective to build a small *domain-specific language* on top of another language like Javascript
* A sub-language can be more expressive in that it is more focused in what it expresses
