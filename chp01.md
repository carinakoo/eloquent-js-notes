# Values, Types, and Operators

### Intro
* All information in a computer is data and is stored as bits
* *Bit*:
  * any representation that has exactly two values such as `0` and `1`
* Binary example:
  * `00001101` = 13.

### Values
* Typical modern computer has more than 30 billion bits in memory, more in hard disk
* *values*: chunks of bits that represent pieces of information
* Each value has a *type* that determines its role
* 6 basic types:
    * numbers
    * strings
    * Booleans
    * objects
    * functions
    * undefined values
* To create a value: invoke its name.
  * Example:
    * `13`
    * Writing and running this in a program causes the bit pattern for the number 13 to be written in somewhere in memory
* As soon as you no longer use a value, it will cease to be stored

### Numbers
* Javascript uses 64 bits to store a number value
* 64 bits can represent 2^64 (18 quintillion) different numbers
* One bit indicates the sign
* Floating or decimal numbers are stored by using some bits to store the position of the decimal point
* You can use scientific notation for writing very large or small numbers (e.g. 2.998e8)

### Arithmetic
* Operators: `+`, `-`, `*`, `/`, `%`
* Order follows mathematical precedence (multiplication/division before addition/subtraction)
* You can use parentheses to control the order of operations
* Remainder operator (% in X % Y) tells you the remainder of dividing X by Y.
  * Often referred to as modulo

### Special Numbers
* `Infinity`, `-Infinity`
* `NaN`
  * Not a number. You get this when you do a numeric operation that doesn’t have a meaningful result, like 0/0.

### Strings
* Represents text
* Some special characters such as quotes and newlines must be escaped with a preceding backslash
  * Example: a newline must be escaped
    * The following code represents this string:
      * "A newline character is written like "\n"."
    * `"A newline character is written like \"\\n\"."`

### Unary Operators
* `typeof`, `-`
* Take only one value
* `typeof` returns a string representing the type of the value

### Boolean Values
* `true`, `false`

### Comparisons
* `<`, `>`, `==`, `!=`, `<=`, `>=`
* Strings can be compared
    * Uppercase letters “lower” than lowercase letters
    * Based on unicode standard (every character assigned a number)
* `NaN` is not equal to itself

### Logical Operators
* `&&`, `||`, `!`
* Apply to boolean values
* Precedence order: [comparison operators], `&&`, `||`
* “conditional” ternary operator: `?` `:`

### Undefined Values
* `null`, `undefined`
* Returned by operations that don’t produce a meaningful value
* undefined and null are usually interchangeable

### Automatic Type Conversion
* *type coercion*:
  * When an operator is applied to the “wrong” type, JS converts it to the type it wants
    ```
    console.log(8 * null)
    // → 0
    ```
* `null` and `undefined` are only equal to `null` or `undefined`, not `0`
  ```
  null == undefined
  // true
  null != 0
  // false
  ```
* Compare `x == null` to test whether a value has a real value
* `0`, `NaN`, `""` count as false
* Use `===` and `!==` to compare without type conversion. Use defensively to catch unexpected type conversions

### Short-circuiting of logical operators
* `&&`
    * if left side evaluates as false, it is returned without evaluating right side
    * if left side evaluates as true, right side value is returned
* `||`
    * if left side evaluates as true, it is returned without evaluating right side
    * if left side evaluates as false, right side value is returned
* Right side value only evaluated when necessary
* Conditional (ternary) operator
    * 1st first expression always evaluated
    * Whichever of 2nd or 3rd expression not picked is not evaluated
