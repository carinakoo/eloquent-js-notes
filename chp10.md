# Modules
> A beginning programmer writes her programs like an ant builds her hill, one piece at a time, without thought for the bigger structure. Her programs will be like loose sand. They may stand for a while, but growing too big they fall apart.
>
Realizing this problem, the programmer will start to spend a lot of time thinking about structure. Her programs will be rigidly structured, like rock sculptures. They are solid, but when they must change, violence must be done to them.
>
The master programmer knows when to apply structure and when to leave things in their simple form. Her programs are like clay, solid yet malleable.
>
-- Master Yuan-Ma, *The Book of Programming*

* Modules divide programs into clusters of code that, by some criterion, belong together.

### Why modules help
* Structure helps people who aren't familiar with the code find what they're looking for
* Structure makes it easier for the programmer to keep things that are related close together.
* *literate programming*: programs are organized in a model similar to traditional text, with well-defined order for reading and accompanying explanation in the form of comments
* adding structure costs energy; it's best not to add structure at an early stage

### Namespacing
* JavaScript does not have a scope level between global and local
   * everything outside of top level functions can be seen everywhere in the program
* *Namespace pollution*: the problem of a lot of unrelated code having to share a single set of global variable names
* Prior to JS providing a module construct, objects can be used to create subnamespaces
* Functions can be used to create private namespace inside a module

### Reuse
* Organizing coherent pieces of functionality into separate files makes these pieces easier to manage and reuse
* When relationships between modules are explicitly stated, you can automate the process of installing and upgrading them
* NPM is a tool fo this

### Decoupling
* Modules can isolate code, providing a stable public interface to internal functionality whose implementation may change.
* A good module interface exposes as few of the module's internal concepts as possible while making the "language" exposed by the interface flexible enough to be applicable in a wide range of situations

### Using functions as namespaces
* (pre-ES2015) Only functions create their own scope, so we create modules based on functions
* A function can be used to create a completely encapsulated namespace by enclosing a function expression in parentheses, allowing it to be immediately called or invoked


    (function() {
      function someFunction(x) { return x; }
      var someVar = 1;
    })();

### Objects as interfaces
* A pattern in which a module function takes an export object as an argument and appends methods to the object which comprise the module interface


    (function(exports) {
      var names = ["Sunday", "Monday", "Tuesday", "Wednesday",
                 "Thursday", "Friday", "Saturday"];

      exports.name = function(number) {
        return names[number];
      };
      exports.number = function(name) {
        return names.indexOf(name);
      };
    })(this.weekDay = {});

    console.log(weekDay.name(weekDay.number("Saturday")));
    // → Saturday
* This allows you to expose multiple methods as part of the module

### Detaching from the global scope
* Two problems to solve:
  * loading 2 versions of a module
  * loading 2 modules with the same name
* Solution: a `require` function which will load the appropriate module functionality, without using the global scope
* Added benefit: makes dependencies explicit

### Evaluating data as code
* eval does not create a new scope for the code passed as its argument
* Instead, use the Function constructor


    var plusOne = new Function("n", "return n + 1;");
    console.log(plusOne(4));
    // → 5

### Require
* Keep a cache of modules that have already been loaded
* Provide a parent object of the exports property named `module` with property `exports`, so that the module can overwrite the exports object itself, rather than only being able to modify the properties of the exports object.
* This style of module system is called *CommonJS modules* and is built into Node.js

### Slow-loading modules
* Using modules in the browser comes with its own set of challenges
* Loading modules that require fetching from a remote server takes time and by default blocks the whole page from continuing
* *Browserify* is a tool is used in development that loads and packages your dependencies into a single file so that modules are readily available before your code is run by the browser.
* *Asynchronous Module Definition* is a style where the module code is wrapped in an outer function which is called after loading the module's dependencies in the background.
* *RequireJS* is one implementation of this style
* A Basic version of AMD's `define` function for defining modules:


    function define(depNames, moduleFunction) {
      var myMod = currentMod;
      var deps = depNames.map(getModule);

      deps.forEach(function(mod) {
      if (!mod.loaded)
        mod.onLoad.push(whenDepsLoaded);
      });

      function whenDepsLoaded() {
        if (!deps.every(function(m) { return m.loaded; }))
          return;

        var args = deps.map(function(m) { return m.exports; });
        var exports = moduleFunction.apply(null, args);
        if (myMod) {
          myMod.exports = exports;
          myMod.loaded = true;
          myMod.onLoad.forEach(function(f) { f(); });
        }
      }
      whenDepsLoaded();
    }

* Notes:
  * `define` functions uses a helper`getModule` function
    * keeps a cache of loaded modules
    * initializes module objects with `loaded` and `onLoad` properties
    * asynchronously reads in the module file
  * `define` function:
    * Every module including the main program, and every dependency must call this function, resulting in a kind of call stack of dependency handling.
      * As the deepest dependencies are loaded, they callback to their dependents, which then load and call back to their dependents, until all dependencies are loaded and the main module runs.
    * gives each dependency this module's `whenDepsLoaded` function to call when the dependency has loaded
    * the `whenDepsLoaded` function waits until all deps have loaded, then calls this module's own code, updates its `loaded` property to true and calls its `onLoad` function

### Inteface design
* Designing interfaces is a subtle practice requiring insight
* The best way to learn is through experience with lots of interfaces

#### Predictability
* You want programmers to be able to predict the way your inteface works so they don't lose time looking up docs
* Use conventions
* For example, follow conventions from standard JS interfaces
* Don't try to be clever at the expense of ease of use

#### Composability
* Make functions do a single, clear things
* Make functions and use data structures that can potentially interact with other systems, avoiding custom data types

#### Layered interfaces
* To address the tradeoff between giving users more control vs an easier to use interface, you can provide two interfaces: a *high-level* one and a *low-level* one
* The high-level interface can usually be built using the low-level one
