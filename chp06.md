# Chapter 5: The Secret Life of Objects

### History
* Objects are one answer to the problem of complexity
* Object-oriented programming solves the problem by separating complexity into *objects* which provide an *interface* through which they are used
* OO was developed in the 70s-80s and then hugely hyped in the 90s
* Since then, popular opinion has swung back away from OO programming
* Haverbeke prefers practical rather than ideological attitude to the differing approaches
* Javascript has an eccentric take on objects

### Methods
* *methods*: object properties that hold function values
* *this* keyword in method body points to the object the method was called on
* *apply*, *bind*, and *call*
	* methods on function objects
	* first argument is the object assigned as the value of *this*
* *call* is like apply but takes a normal list of arguments (x, y, z) rather than an array ([x, y, z])

### Prototypes
* prototypes
	* almost all objects have a prototype
	* used as a fallback source of properties
	* used as container for properties shared by all objects of that prototype
	
* individual objects
	* individual object properties apply only to the object
	* shared properties derived from prototype
* Default prototypes:
	* `Object.prototype` 
		* default prototype of most objects. 
		* provides some methods that show up in all objects, such as `toString`
	* `Function.prototype`: default function prototype
	* `Array.prototype`: default array prototype
	* `Function.prototype` and `Array.prototype` have prototype `Object.prototype`
* `Object.getPrototypeOf` returns an object's prototype
* `Object.create`: create object with a given prototype

### Constructors
* `new`
	* calling a function with the `new` keyword in front of it causes it to be treated as a constructor
	* the constructor will have `this` bound to a fresh object, which will be the default returned value
* an object created with `new` is an *instance* of its constructor
* By convention constructor names are capitalized
* `prototype` property
	* By default an empty object with prototype `Object.prototype`
	* Objects created with the constructor will have the `prototype` object as their prototype
	* Distinct from the constructors own prototype, which is `Function.prototype`
	
### Overriding derived properties
* Individual object properties override object prototype properties with the same name for that object
* Used to express exceptional properties in instances of a more generic class of objects

### Prototype interference
* Prototype properties declared by standard assignment may produce problems when they are counted along with the conceptual properties of the individual object
* Two ways to distinguish between prototype properties and individual object properties
	* `Object.defineProperty` allows you to declare prototype properties as nonenumerable (they won't show up in a for/in loop)
	* `Object.hasOwnProperty` tells whether the property exists on the individual object as opposed to the prototype
	
### Prototype-less objects
* pass `null` to Object.create to creat an object without a prototype

### Polymorphism
* *polymorphism*: when code is written to support one interface for multiple kinds of objects (shapes)

### Laying out a table
* An example program prints out a table from an array of content data
* Prototypes used to represent different styles of cells
* Cell methods provide info about their height and width, and draw the cell itself

### Getters and Setters
* object literals have `get` and `set` notation that specify functions to be run when a property is read or written
* this functionality is also provided by `Object.defineProperty`
* When a getter is defined without a setter, the property is unwriteable

### Inheritance
* In *inheritance*, a new constructor builds on the code of an existing constructor by 
	* calling the existing constructor using `call`
	* assigning its prototype to an object whose prototype is the existing constructor's `prototype` object
* Objects created by the new constructor derive properties from the existing constructor
* The new constructor's prototype properties can override its derived properties
* Inheritance is controversial
	* often confused with polymorphism
	* often overused
	* increases interdependency between different pieces of code
	* use with caution
	* *composition* may often be preferable
		* store the derived object in a property and refer to it from methods

### The instanceof operator
* `instanceOf`
	* binary operator returns true if object was derived from given constructor
	* sees through inherited types




