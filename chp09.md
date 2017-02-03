# Chapter 9 Regular Expressions

### Creating a Regular Expression
* Two syntaxes for declaring a regular expression


    var re1 = new RegExp("abc");
    var re2 = /abc/;

* backslashes preceding special characters escape the characterso
* other backslashes will be considered part of the pattern

### Testing for matches
* The simplest method on regular expressions is `test`


  console.log(/abc/.test("abcde"));


* Returns true if 'abc' occurs anywhere in the test string

### Matching a set of characters
* Brackets
  * match any character between brackets
  * a dash (`-`) indicates a range according to characters' Unicode number

    console.log(/[0123456789]/.test("in 1992"));
    // → true
    console.log(/[0-9]/.test("in 1992"));
    // → true


* Character groups
  * `\d` digits
  * `\w` alphanumeric
  * `\s` spaces
  * `\D` not a digit
  * `\W` not a alphanumeric
  * `\S` not a space
  * `.` any character except newline
* *invert* a character set using a caret (`^`) after opening bracket

### Repeating parts of a pattern
* `+` matches the preceding pattern occurring 1 or more consecutive times
* `*` matches the preceding pattern occurring 0 or more times
* `?` makes the preceding pattern optional
* `{4}` matches preceding pattern occurring 4 times
* `{4,8}` matches preceding pattern occurring 4-8 times
* `{4,}` matches preceding pattern occurring 4 or more times

### Grouping subexpressions
* use parentheses to create subexpressions that can be handled as a group
    let laugh = /Ha(ha)+/;

### Matches and groups
* `exec`: method on regular expressions
  * returns null if no match found
  * returns object with match info if match found
  * return object's `index` property tells where the match begins
  * rest of return object is array of strings
    * first element is string matched
    * following elements are matched subgroups, if any
    * unmatched subgroups have property `undefined`
    * when a group has multiple matches, only the last one is kept in the result array

### The date type
* `Date` is a standard JavaScript object type


    new Date();
    new Date(2009, 11,9);
    // → Wed Dec 09 2009 00:00:00 GMT+0100 (CET)

    new Date(1387407600000);

  * Months are 0 indexed
  * Days are 1 indexed
  * Timestamps are the number of milliseconds since the start of 1970
  * Negative numbers for before 1970
  * Date.now: current timestamp
  * Date object properties
    * getTime
    * getFullYear
    * getMonth
    * getDate
    * getHours
    * getMinutes
    * getSeconds

### Word and string boundaries
* `^` and `$` are markers for the beginning and end of the input string
* `\b` marks a word boundary (either the start or end of the string, or a point with a word character (alphanumeric) and a nonword character together)

### Choice patterns
* `|` denotes a choice between two patterns

### The mechanics of matching
* The regex engine starts at the beginning of the string and tries a match there
* If a match is found, it moves along to find a match for the next part of the pattern
* If no match is found, it moves forward to the next character in the test string to look for a match
* It repeats this process until the full pattern is matched or it concludes that there is no match

### Backtracking
* *backtracking* can be a problem when certain patterns cause the matcher to reprocess a part of the tested string multiple times
* this can cause a match to take a long time

### The replace method
* `replace`: method on String types
* a regex followed by `g` indicates the *global* option, in which all matches of the pattern in the string will be replaced
* The replacement string can refer back to matched groups using numbered variables `$1`, `$2`, `$3` and so on.
* `$&` refers to the whole match
* A function may be used as the argument for the replacement string
  * The function is called with the whole match and matched groups as arguments
  * The returned value is used as the replacement string

### Greed
* By default, repetition operators try to match as much as they can. They will start by trying to match the rest of the string and if it does not match, move back one character and try again
* Adding a question mark after the these operators flips this behavior, making them nongreedy. They will try to match as little as possible and only match more if the smaller match fails.
* `+?`
* `*?`
* `??`
* `{}?`
* Greedy repetition operators often cause bugs. You should usually try nongreedy operators first.

### Dynamically creating RegExp objects
* Example:


    var regexp = new RegExp("\\b(" + name + ")\\b", "gi");

* Special characters with backslash such as `\b` require 2 backslashes (`\\b`) since you are using regular string notation, not regular expression notation.
* Second argument is string of regex options like `"gi"`
* In order to dynamically include characters which may also be regex special characters like `+` or `[]`, escape any characters that are not alphanumeric or whitespace (escaping alphanumeric characters would result in unintended special characters; escaping spaces would result in matching backslash character):


    var name = "dea+hl[]rd";
    var text = "This dea+hl[]rd guy is super annoying.";
    var escaped = name.replace(/[^\w\s]/g, "\\$&");
    var regexp = new RegExp("\\b(" + escaped + ")\\b", "gi");

### The search method
* `search`: method on strings which takes a regular expression and returns first index where expression is found, or -1 if not found

### The lastIndex property
* Regular expressions object properties include:
  * `source`: the string from which the regex was created
  * `lastIndex`: when the global option `g` is set, the `exec` method will use `lastIndex` as the starting index for the match.
    * After a match is made, `lastIndex` is updated to the next the point after the match
    * If no match, `lastIndex` reset to 0
    * This can cause unintended behavior when calling `exec` multiple times on a pattern
* The global option also changes the return object from the string `match` method.
  * Instead of returning the typical result object (matched string followed by matched subgroups), `match` will return an array containing all matched strings

### Looping over matches
* A common pattern is to loop through occurrences of a pattern in a string in a way which provides access to the match object using `lastIndex` and `exec`:


    var input = "A string with 3 numbers in it... 42 and 88.";
    var number = /\b(\d+)\b/g;
    var match;
    while (match = number.exec(input))
    console.log("Found", match[1], "at", match.index);
    // → Found 3 at 14
    //   Found 42 at 33
    //   Found 88 at 40

* The value of an assignment expression (=) is the assigned value

### Parsing an INI file
* Example program
* Use `/\r?\n/` to match newline characters and optional carriage returns for some operating systems
* Loop through lines and match each line, creating an array of settings and throwing an exception for lines that fail to match
* Use `^` and `$` to make sure to match whole lines, avoiding possible bugs

### International characters
* For historical reasons, JavaScript's implementation of regexes fails to recognize some non-English characters such as characters with accents, which will match `\W`, the nonword category
* However, the implementation of `\s` does recognize all Unicode whitespace characters including those of other languages
* Some regex implementations in other programming languages have syntax for matching Unicode categories such as "all uppercase letters", "control characters", however this may take a long time to be implemented in JS
