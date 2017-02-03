# Program Structure

### Expressions and Statements
* expression: a fragment of code that produces a value
* expressions can be combined and nested into more complex expressions
* statement: like a full sentence
* the simplest statement is just an expression followed by a semicolon
* A statement has little meaning unless it changes state in a way that affects future statements
* side effects: change to state in a way that affects future statements
* There are complex rules allowing the omission of semi-colons in certain contexts. It’s best to use semi-colons consistently until you understand the rules well.

### Variables
* variables provide pointers to stored values
* variable names
    * can be any word that isn’t a reserved word
    * can have digits but may not start with a digit
    * cannot include punctuation except for `$` and `_`
* variables point to values, do not contain them. 2 variables can refer to the same value
* you can define multiple variables with one statement (var one = 1, two = 2;)

### Keywords and Reserved Words
* keywords cannot be used as variable names.
* some keywords are reserved for future versions of javascript

### The Environment
* environment: the collection of variables and their values that exist at a given time
* every program starts with some standard variables set
    * variables that are part of the language standard
    * variables that enable interaction with surrounding system such as the current document or user input

### Functions
* Many environment variables are functions
* A function is a piece of program wrapped in a value
* Executing a function is called invoking, calling, or applying
* arguments: values given to functions

### Console.log
* writes out arguments to a text output device

### Return Values
* Functions may change the program state by producing side effects or returning values
* Function calls are expressions

### Prompt and Confirm
* Like “alert” but confirm has OK/Cancel buttons and prompt has user input

### Control Flow
* Straight control flow executes statements one by one top to bottom

### Conditional Execution
* if/else: Checks condition and chooses path based on check

### While and Do Loops
* block: a group of statements wrapped in braces
* do loop: always executes body at least once; starts testing condition after first execution

### Indenting Code
* indentations and line breaks are optional and used for readability

### For Loops
* 3 parts:
    * initialize: define a variable,
    * check: check condition,
    * update: update state after every iteration

### Breaking out of a loop
* break: immediately jump out of the enclosing loop
* continue: jumps out of body and continue with the next iteration

### Updating Variables Succinctly
* +=, -=, ++, —

### Dispatching on a value with switch
* starts executing on the corresponding case statement and continues until reaching a “break” statement

### Capitalization
* camelCase convention
* capitalizing a function marks it as a constructor by convention

### Comments
* ignored by computer
* single line (`//`), multiline(`/**/`)
