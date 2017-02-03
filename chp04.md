# Data Structures: Objects and Arrays

### Intro
* Objects group values together

### The Weresquirrel
* In the example, Jacques is a person who turns into a squirrel in the evening on some evenings, and he is trying to figure out what behavior causes the transformation. He uses data and correlation computation to determine which of his activities correlates with the times he transforms into a squirrel.

### Data Sets
* array: a data type for storing sequences of values

### Properties
* almost all javascript values have properties except null and undefined
* elements in arrays are stored in properties
* property names that are not valid variable names must be accessed using square brackets instead of dot notation

### Methods
* methods: properties that contain functions are called methods of the value they belong to
* push: adds values to the end of an array
* pop: removes one value from end of array and returns it
* join: flattens an array of strings into a single string, using the passed string argument as glue between the array’s string elements

### Objects
* objects: arbitrary collections of properties
* properties whose names are not valid variable names or numbers must be quoted
* delete removes a property from an object
* in operator indicates whether an object has a certain property
* if the property value is “undefined” the value (property in object) is still true
* arrays are just specialized objects

### Mutability
* basic values (string, number) are immutable. objects are mutable.
* 2 variables can point to the same object, but two objects with the same properties and values are not necessarily the same object

### The Lycanthrope’s Log
* Jacque uses javascript to record his activities. For each day he records an entry object which includes an array of his activities that day and a boolean representing whether or not he turned into a squirrel that day.
* When he has enough data points (entries), he will compute the correlation coefficient (phi) for each of his activities.

### Computing Correlation
* To compute the coefficient, each of the activities needs a corresponding data set recording the number of occurrences of the activity relative to occurrences of the squirrel transformation
* indexOf: searches for a given value in the array and returns the index if found
* This data set is represented with an array, where the binary representation of the indices represents an occurrence combination of squirrel transformation and activity. For example, the index “2" in binary is “10”, representing occurrences where the squirrel transformation happened (left bit) but the activity (right bit) did not.
* This array is created by looping through each entry and setting the corresponding occurrence bit.

### Objects as Maps
* map: a way to go from values in one domain to corresponding values in another domain
* a map of the phi values maps from even names to phi values
* loop over a map using in: “for var event in map”

### Final Analysis
* Looking through the phi correlations, there are 2 which are significantly higher than the others: “peanut” has a significantly high positive correlation and “brushed teeth” has a high negative correlation
* We create a new event for when the two co-occur: “peanuts” and “not brushed teeth”, and this new combined event has a correlation of 1. Thus the mystery is solved: Jacques turns into a squirrel when he eats peanuts and doesn’t brush his teeth.

### Further Arrayology
* shift: remove an element from the beginning of the array and return it
* unshift: add an element to the beginning of the array
* lastIndexOf: searches for an element from the end of the array and returns the index if found
* slice: returns elements of an array between the given indices
* concat: glues arrays together

### Strings and Their Properties
* Strings have built-in properties: slice, indexOf, trim, charAt

### The Arguments Object
* Whenever a function is called, a special variable named arguments is added to the environment in which the function body runs
* arguments object has a length property that tells the number of arguments actually passed
* has properties 0, 1, 2… for each argument BUT does not have typical array properties like slice or indexOf
* this dynamic nature of the arguments object allows for functions to take an arbitrary number of arguments and just loop over the arguments object to access them

### The Math Object
* a grab-bag of number-related utility functions
* Math provides a namespace so these functions do not have to be global variables
* javascript will not warn you if you define a variable with a name that already exists
* trigonometry functions: cos, sin, tan, Math.PI
* Math.random: psueudo random number between 0 and 1 created by complex computations simulating randomness
* Math.floor, Math.ceil, Math.round

### The Global Object
* global scope can be accessed as an object
* global variables stored as properties on this object
