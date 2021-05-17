# What is JavaScript?
JavaScript (JS) is a lightweight interpreted or JIT-compiled programming language with first-class functions.


# What are JavaScript data types?
In JavaScript, a primitive (primitive value, primitive data type) is data that is not an object and has no methods. There are 6 primitive data types: string, number, boolean, null, undefined, symbol (new in ECMAScript 2015).

All primitives are immutable, i.e., they cannot be altered. It is important not to confuse a primitive itself with a variable assigned a primitive value. The variable may be reassigned a new value, but the existing value can not be changed in the ways that objects, arrays, and functions can be altered.

Except for null and undefined, all primitive values have object equivalents that wrap around the primitive values:

* `String` for the string primitive.
* `Number` for the number primitive. (Number is a numeric data type in the double-precision 64-bit floating point format (IEEE 754).)
* `Boolean` for the boolean primitive.
* `Symbol` for the symbol primitive. Symbols are completely unique identifiers. Just like their primitive counterparts (Number, String, Boolean), they can be created using the factory function Symbol() which returns a Symbol. A symbol value may be used as an identifier for object properties; this is the data type's only purpose. [More...](https://medium.freecodecamp.org/how-did-i-miss-javascript-symbols-c1f1c0e1874a)

The wrapper's valueOf() method returns the primitive value.

```javascript
Number(6).valueof()
// 6
```
[More details...](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)


# What are the differences between variables created using let, var or const?
- Scope:
  - var is function or global scoped
  - let and const are block scoped
  - var creates a property on the global object 
  - let/const does not create a property on the global object 
- Hoisting
  - While variables declared with var keyword are hoisted (initialized with undefined before the code is run) which means they are accessible in their enclosing scope even before they are declared
  - let variables are not initialized until their definition is evaluated. Accessing them before the initialization results in a ReferenceError. Variable said to be in "temporal dead zone" from the start of the block until the initialization is processed.
- Redeclaration
  - var will let you re-declare the same variable in the same scope
  - let raises a SyntaxError
- [More on let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [More on const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- [More on var](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)


# Why closure works differently with var and let in below example?
```javascript
// prints '10' 10 times
for (var i = 0; i < 10; i++) { process.nextTick(_ => console.log(i)) }
// prints '0' through '9'
for (let i = 0; i < 10; i++) { process.nextTick(_ => console.log(i)) }
``` 
> Answer:
If you use that let keyword in the for statement, it will check what names it does bind and then
- create a new lexical environment with those names for 
  - the initialiser expression 
  - each iteration (previosly to evaluating the increment expression)
- copy the values from all variables with those names from one to the next environment

for (let i = 0; i < 10; i++) process.nextTick(_ => console.log(i)); does "desugar" to the much more complicated:
```javascript
// using braces to explicitly denote block scopes, // using indentation for control flow
{ let i;
  i = 0;
  __status = {i};
}
{ let {i} = __status;
  if (i < 10)
      process.nextTick(_ => console.log(i))
      __status = {i};
}   { let {i} = __status;
      i++;
      if (i < 10)
          process.nextTick(_ => console.log(i))
          __status = {i};
    }   { let {i} = __status;
          i++;
          …
```
- [ECMA specification](https://262.ecma-international.org/6.0/#sec-createperiterationenvironment)
- [Stackoverflow answer](https://stackoverflow.com/questions/30899612/explanation-of-let-and-block-scoping-with-for-loops)


# What is ‘this’ keyword in JavaScript?
>The `this` keyword refers to the function's execution context. `this` evaluates to the value of the ThisBinding of the current execution context
It has different values depending on where it is used:
- In a method, this refers to the owner object.
- Alone, this refers to the global object.
- In a function, this refers to the global object.
- In a function, in strict mode, this is undefined.
- In an event, this refers to the element that received the event.
- Methods like call(), and apply() can refer this to any object paased as an argument.

- [More on MDN...](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- [More on W3Schools...](https://www.w3schools.com/js/js_this.asp)


# Array.prototype.map()
The map() method creates a new array populated with the results of calling a provided function on every element in the calling array.
```javascript
let numbers = [1, 4, 9]
let roots = numbers.map(function(num) {
    return Math.sqrt(num)
})
// roots is now     [1, 2, 3]
// numbers is still [1, 4, 9]
```
[Know more...](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)


# Array methods
[Know more...](https://www.w3schools.com/jsref/jsref_obj_array.asp)


# Explain event delegation
- The idea is that if we have a lot of elements handled in a similar way, then instead of assigning a handler to each of them – we put a single handler on their common ancestor.
- In the handler we get event.target to see where the event actually happened and handle it.

- [David Walsh blog](https://davidwalsh.name/event-delegate)
- [Dmitri Pavlutin blog](https://dmitripavlutin.com/javascript-event-delegation/)


# Events in detail
[More on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)


# Explain how prototypal inheritance works?
JavaScript objects are dynamic "bags" of properties (referred to as own properties). JavaScript objects have a link to a prototype object. When trying to access a property of an object, the property will not only be sought on the object but on the prototype of the object, the prototype of the prototype, and so on until either a property with a matching name is found or the end of the prototype chain is reached.
- [Know more...](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#inheritance_with_the_prototype_chain)
- [Why prototypical inheritance matters](http://aaditmshah.github.io/why-prototypal-inheritance-matters/)


# Different ways to create objects and the resulting prototype chain:
[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#different_ways_to_create_objects_and_the_resulting_prototype_chain)


# How Pseudoclassical Inheritance works?
[Pseudoclassical Inheritance](https://dev.to/tangweejieleslie/pseudoclassical-inheritance-pattern-in-javascript-1a48)


# What is a closure, and how/why would you use one?
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
[Know more...](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)


# Generators:
Generators are functions that can be exited and later re-entered. Their context (variable bindings) will be saved across re-entrances.
- **Generator function***: The function* declaration (function keyword followed by an asterisk) defines a generator function, which returns a Generator object.
[Generator function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)
- **Generator object**: The Generator object is returned by a generator function and it conforms to both the iterable protocol and the iterator protocol.
[Generator object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator)



# Explain Function.prototype.bind()
[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)


# What's the difference between .call and .apply?
The call() method calls a function with a given this value and arguments provided individually.
[call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
The apply() method calls a function with a given this value, and arguments provided as an array (or an array-like object).
[apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)


# Hoisting:
Hoisting was thought up as a general way of thinking about how execution contexts (specifically the creation and execution phases) work in JavaScript. However, the concept can be a little confusing at first.

Conceptually, for example, a strict definition of hoisting suggests that variable and function declarations are physically moved to the top of your code, but this is not in fact what happens. Instead, the variable and function declarations are put into memory during the compile phase, but stay exactly where you typed them in your code.
[More on MDN](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)


# Function in detail
[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)


# What are async functions?
An async function is a function declared with the async keyword, and the await keyword is permitted within them. The async and await keywords enable asynchronous, promise-based behavior to be written in a cleaner style, avoiding the need to explicitly configure promise chains.
[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)


# function types
- First class functions: A programming language is said to have First-class functions when functions in that language are treated like any other variable. For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable.
- Higher order function: A function that returns a function is called a Higher-Order Function.
- Pure functions: The function return values are identical for identical arguments.


# function currying, partial function, function composition: curring vs composition?


# Functional programming

[Medium blog](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0)


# Callback function
- A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.
- Where callbacks really shine are in asynchronous functions, where one function has to wait for another function (like waiting for a file to load).
- **Callback hell**: Callback hell is when we nest multiple asynchronous operations one after the other. By nesting callbacks in such a way, we easily end up with error-prone, hard to read, and hard to maintain code.


# Nested functions and closures
- You may nest a function within another function. The nested (inner) function is private to its containing (outer) function.
- It also forms a closure. A closure is an expression (most commonly, a function) that can have free variables together with an environment that binds those variables (that "closes" the expression).
- Since a nested function is a closure, this means that a nested function can "inherit" the arguments and variables of its containing function. In other words, the inner function contains the scope of the outer function.
[Closures on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#nested_functions_and_closures)


# Event bubbling and capture:
When an event is fired on an element that has parent elements , modern browsers run two different phases — the capturing phase and the bubbling phase.
- In the capturing phase:
  - The browser checks to see if the element's outer-most ancestor (<html>) has an onclick event handler registered on it for the capturing phase, and runs it if so.
  - Then it moves on to the next element inside <html> and does the same thing, then the next one, and so on until it reaches the element that was actually selected.
- In the bubbling phase, the exact opposite occurs:
  - The browser checks to see if the element selected has an onclick event handler registered on it for the bubbling phase, and runs it if so.
  - Then it moves on to the next immediate ancestor element and does the same thing, then the next one, and so on until it reaches the <html> element.
> [More on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_bubbling_and_capture)


# Difference between document load event and document DOMContentLoaded event?
- The **DOMContentLoaded** event fires when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading.
- A different event, load, should be used only to detect a fully-loaded page. It is a common mistake to use load where DOMContentLoaded would be more appropriate.
- The load event is fired when the whole page has loaded, including all dependent resources such as stylesheets and images. This is in contrast to DOMContentLoaded, which is fired as soon as the page DOM has been loaded, without waiting for resources to finish loading.


# Why would you use something like the load event? Does this event have disadvantages? Do you know any alternatives, and why would you use those?


# Explain the same-origin policy with regards to JavaScript.
The same-origin policy is a critical security mechanism that restricts how a document or script loaded from one origin can interact with a resource from another origin. It helps isolate potentially malicious documents, reducing possible attack vectors.
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)


# What is "use strict";? what are the advantages and disadvantages to using it? 
JavaScript's strict mode, introduced in ECMAScript 5, is a way to opt in to a restricted variant of JavaScript
Advantages:
- Strict mode makes it easier to write "secure" JavaScript.
- Strict mode changes previously accepted "bad syntax" into real errors.
- As an example, in normal JavaScript, mistyping a variable name creates a new global variable. In strict mode, this will throw an error, making it impossible to accidentally create a global variable.
- In normal JavaScript, a developer will not receive any error feedback assigning values to non-writable properties.
- In strict mode, any assignment to a non-writable property, a getter-only property, a non-existing property, a non-existing variable, or a non-existing object, will throw an error.
> [More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)


# Promises:
The Promise object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.
```javascript
new Promise((resolve, reject) => {
    reject();
})
.then(() => {
    console.log('Success callback! on resolve');
})
.catch(() => {
    console.error('Error callback, on reject');
})
.then(() => {
    console.log('Always lands here, no matter what happened before');
});
```
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)


# Spread operator vs rest argument
When using spread, you are expanding a single variable into more:
```javascript
var abc = ['a', 'b', 'c'];
var def = ['d', 'e', 'f'];
var alpha = [ ...abc, ...def ];
console.log(alpha)// alpha == ['a', 'b', 'c', 'd', 'e', 'f'];
```
When using rest arguments, you are collapsing all remaining arguments of a function into one array:
```javascript
function sum( first, ...others ) {
    for ( var i = 0; i < others.length; i++ )
        first += others[i];
    return first;
}
console.log(sum(1,2,3,4)) // sum(1, 2, 3, 4) == 10;
```


# What are ES6 features?
ES6 includes the following new features:
- arrows
- classes
- enhanced object literals
- template strings
- destructuring
- default + rest + spread
- let + const
- iterators + for..of
- generators
- unicode
- modules
- module loaders
- map + set + weakmap + weakset
- proxies
- symbols
- subclassable built-ins
- promises
- math + number + string + array + object APIs
- binary and octal literals
- reflect api
- tail calls


# Event loop:
[Read on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)


# What is spread operator?
Spread syntax (...) allows an iterable such as an array expression or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.
[Know more](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)


# Asynchronous JavaScript 
[Know more](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous)


# Keyed collections, Indexed collections
- Keyed collections [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Keyed_collections)
  - Map
    ECMAScript 2015 introduces a new data structure to map values to values. A Map object is a simple key/value map and can iterate its elements in insertion order.
    ```javascript
    let sayings = new Map();
    sayings.set('dog', 'woof');
    sayings.set('cat', 'meow');
    sayings.size; // 2
    sayings.get('dog'); // woof
    sayings.get('fox'); // undefined
    sayings.has('bird'); // false
    sayings.delete('dog');
    sayings.has('dog'); // false

    for (let [key, value] of sayings) {
      console.log(key + ' goes ' + value);
    }
    // "cat goes meow"
    // "elephant goes toot"
    sayings.clear();
    sayings.size; // 0
    ```
  - Set
    Set objects are collections of values. You can iterate its elements in insertion order. A value in a Set may only occur once; it is unique in the Set's collection.
    ```javascript
    let mySet = new Set();
    mySet.add(1);
    mySet.add('some text');
    mySet.add('foo');

    mySet.has(1); // true
    mySet.delete('foo');
    mySet.size; // 2

    for (let item of mySet) console.log(item);
    // 1
    // "some text"
    ```
- Indexed collections [Know more](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections)
  - Array
    An array is an ordered list of values that you refer to with a name and an index.
  - Typed Array
    JavaScript typed arrays are array-like objects and provide a mechanism for accessing raw binary data.


# JavaScript Accessors (Getters and Setters)
The getter and setter keyword are used for accessing the objects. The getter return value is used when a property is being accessed and the setter takes an argument and sets the property value inside the object to that passed argument.
```JAVASCRIPT
// Create an object:
var person = {
  firstName: "John",
  lastName : "Doe",
  language : "",
  set lang(lang) {
    this.language = lang;
  },
  get lang() {
    return this.language;
  }

};
// Set an object property using a setter:
 person.lang = "en";
// Display data from the object using a getter:
console.log(person.lang); // en
```
[W3Schools](https://www.w3schools.com/js/js_object_accessors.asp)


# Lexical vs dynamic scope
- JavaScript does not, in fact, have dynamic scope. It has lexical scope. But the `this` mechanism is kind of like dynamic scope.
- The key contrast: lexical scope is write-time, whereas dynamic scope (and `this`!) are runtime. Lexical scope cares where a function was declared, but dynamic scope cares where a function was called from.
- Finally: `this` cares how a function was called, which shows how closely related the `this` mechanism is to the idea of dynamic scoping.


# Global, local block scope
- The Global scope
  A variable exists inside or outside a block. If a variable is declared outside all functions or curly braces ({}), it exists in the global scope. The global variables can be accessed by any line of code in the program, including inside blocks.
- The Local scope
  In contrast to global variables, locally scoped ones are only visible within the function they are declared. Each function written in JavaScript creates a new local scope and every variable declared in this scope is a local variable. That means that variables with the same name can be used in different functions. However, any effort to reference a local variable outside its scope will result in a Reference Error.
- The Block scope
  - So far, we’ve seen variables defined with the var keyword. Var can declare a variable either in the global or local scope. The variables that are declared within the block scope are comparable to local ones. They are available within the block that they are defined.
  - The main difference between the local scope and block scope is that the block statements (e.g. if conditions or for loops), don't create a new scope. So the var keyword will not have an effect, because the variables are still in the same scope.
  - ES6 introduced block scope by using the let and const keywords. These two keywords are scoped within the block which are defined.
> [More on dev.io](https://dev.to/ale3oula/the-hor-r-o-r-scope-global-local-and-block-scope-in-js-37a1#:~:text=The%20Block%20scope&text=Var%20can%20declare%20a%20variable,block%20that%20they%20are%20defined.)


# Variable masking
Transforming variable value to hide its original value. ***Needs modification***


# Variable shadowing
In computer programming, **variable shadowing** occurs when a variable declared within a certain scope (decision block, method, or inner class) has the same name as a variable declared in an outer scope.


# IIFE
An IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined. 
[MDN](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)


# Interface


# *Async & await


# How many ways we can create object


# How can we achieve multithreading in JavaScript?


# Angular expression vs Javascript expression


# Exceptions & error handling
The try statement consists of a try-block, which contains one or more statements. {} must always be used, even for single statements. At least one catch-block, or a finally-block, must be present. This gives us three forms for the try statement:
- try...catch
- try...finally
- try...catch...finally
```javascript
try {
  try_statements // The statements to be executed.
} catch (e) { // e: An optional identifier to hold an exception object for the associated catch-block.
  if (e instanceof TypeError) {
    // statements to handle TypeError exceptions
  } else if (e instanceof RangeError) {
    // statements to handle RangeError exceptions
  } else if (e instanceof EvalError) {
    // statements to handle EvalError exceptions
  } else {
    // statements to handle any unspecified exceptions
  }
} finally {
  finally_statements // Statements that are executed after the try statement completes. These statements execute regardless of whether an exception was thrown or caught.
}
```
- throw
  - The 'throw' statement throws a user-defined exception. Execution of the current function will stop (the statements after throw won't be executed), and control will be passed to the first catch block in the call stack. If no catch block exists among caller functions, the program will terminate.
  - You can use throw to rethrow an exception after you catch it
```javascript
throw 'Error2'; // generates an exception with a string value
throw 42;       // generates an exception with the value 42
throw true;     // generates an exception with the value true
throw new Error('Required');  // generates an error object with the message of Required
```
- Error() constructor syntax:
```javascript
new Error()
new Error(message)
new Error(message, fileName)
new Error(message, fileName, lineNumber)
```
Read more on MDN:
- [Error object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
- [List of Errors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors)
- [try...catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)
- [throw](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw)


# What are falsy values in javascript?
The following values evaluate to false (also known as Falsy values):
- false
- undefined
- null
- 0
- NaN
- the empty string ("")


# 90. Events:
# 91. Async programming
# 93. Promises
# 96. Ajax & JQuery
# 97. valueof and unboxing
# 98. How to find memory leaks in JavaScript?
# 99. JavaScript memory management
# 100. Applications caching
# 101. Service worker
# What are web workers?
# Cookies?

# Identifiers
# 47.	Literals
# 48.	Primitive types & objects
# 49.	Numbers=> Math
# 50.	Strings
# 51.	Special characters
# 52.	Booleans
# 53.	Symbols
# 54.	Regular expressions
# 55.	Objects
# 57.	Trailing commas in Objects n Arrays
# 58.	Dates
# 60.	Data type conversion/Coersion
# 61.Control flow statements and flow patterns
# 62.Expressions and Operators

# memoization


# Debouncing and Throttling in JavaScript
- **Throttling** will delay executing a function. It will reduce the notifications of an event that fires multiple times.
- **Debouncing** will bunch a series of sequential calls to a function into a single call to that function. It ensures that one notification is made for an event that fires multiple times.
[Read more](https://davidwalsh.name/function-debounce)


# Destructuring? How to do destructuring for Objects?
The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.
```javascript
// Array destructuring

// Object destructuring
const hero = {
  name: 'Batman',
  realName: 'Bruce Wayne'
};

const { name, realName } = hero;

name;     // => 'Batman',
realName; // => 'Bruce Wayne'
```


# 67.	Pass by value n pass by reference
# 69.	Arrow notation
# 71. Scope:

# 32.What are the pros and cons of using Promises instead of callbacks?
# 33.What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?
# 34.What tools and techniques do you use debugging JavaScript code?
# 35.What language constructions do you use for iterating over object properties and array items?
# 36.Explain the difference between mutable and immutable objects.
# 37.Explain the difference between synchronous and asynchronous functions.
# 38.What is event loop? What is the difference between call stack and task queue?
# 40. What is MonkeyPatching?


# What is Error Object? What are runtime Errors in javascript?
**Error objects** are thrown when runtime errors occur. The Error object can also be used as a base object for user-defined exceptions. See below for standard built-in error types.
- EvalError: Creates an instance representing an error that occurs regarding the global function eval().
- RangeError: Creates an instance representing an error that occurs when a numeric variable or parameter is outside of its valid range.
- ReferenceError: Creates an instance representing an error that occurs when de-referencing an invalid reference.
- SyntaxError: Creates an instance representing a syntax error.
- TypeError: Creates an instance representing an error that occurs when a variable or parameter is not of a valid type.
- URIError: Creates an instance representing an error that occurs when encodeURI() or decodeURI() are passed invalid parameters.
- AggregateError: Creates an instance representing several errors wrapped in a single error when multiple errors need to be reported by an operation, for example by Promise.any().
- InternalError: Creates an instance representing an error that occurs when an internal error in the JavaScript engine is thrown. E.g. "too much recursion".


Performance Questions:

# What tools would you use to find a performance bug in your code?
#  What are some ways you may improve your website's scrolling performance?
# Explain the difference between layout, painting and compositing.


Network Questions:
# Traditionally, why has it been better to serve site assets from multiple domains?
# What are the differences between Long-Polling, Websockets and Server-Sent Events?
# Do your best to describe the process from the time you type in a website's URL to it finishing loading on your screen.
# Explain the following request and response headers:
# Diff. between Expires, Date, Age and If-Modified-...
# Do Not Track
# Cache-Control
# Transfer-Encoding
# ETag
# X-Frame-Options
# What are HTTP methods? List all HTTP methods that you know, and explain them.

# References:
# 1. Primitives: 
https://javascriptweblog.wordpress.com/2010/09/27/the-secret-life-of-javascript-primitives/
# 2. Memory Heap or stack: 
https://hashnode.com/post/does-javascript-use-stack-or-heap-for-memory-allocation-or-both-cj5jl90xl01nh1twuv8ug0bjk
# 3. Stack size:
https://glebbahmutov.com/blog/javascript-stack-size/
# 4. Memory management:
https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec
# 5. Performance tuning:
https://medium.com/@spp020/44-quick-tips-to-fine-tune-angular-performance-9f5768f5d945
# 6. Code review:
https://www.evoketechnologies.com/blog/code-review-checklist-perform-effective-code-reviews/
https://gist.github.com/blakewest/10049924
# 7. Interview questions:
https://www.code-sample.com/2018/04/angular-7-interview-questions-and.html?m=1
# 8. Time saving tips: 
https://blog.angularindepth.com/beware-angular-can-steal-your-time-41fe589483df

# Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?



# 26.Why is it called a Ternary expression, what does the word "Ternary" indicate?
# 23.Why is extending built-in JavaScript objects not a good idea?
# 15.When would you use document.write()?
# 16.What's the difference between feature detection, feature inference, and using the UA string?
# 17.Explain Ajax in as much detail as possible.
# 18.Explain how JSONP works (and how it's not really Ajax).
# 19.Have you ever used JavaScript templating?
# Caching and storages


# 12.Difference between: function Person(){}, var person = Person(), and var person = new Person()?


# 11.What's the difference between host objects and native objects?


# What do you think of AMD vs CommonJS?


# What's the difference between a variable that is: null, undefined or undeclared?


# What is garbage collection in javascript?



# Mixin
A mixin is a class (interface, in WebAPI spec terms) in which some or all of its methods and/or properties are unimplemented, requiring that another class or interface provide the missing implementations. The new class or interface then includes both the properties and methods from the mixin as well as those it defines itself. All of the methods and properties are used exactly the same regardless of whether they're implemented in the mixin or the interface or class that implements the mixin.



# Multiple inheritance
An object can inherit the properties and values from unrelated parent objects. JavaScript does not support multiple inheritance.
> [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Details_of_the_Object_Model#no_multiple_inheritance)
Multiple inheritance can be achieved in ECMAScript 6 by using Proxy objects:
```javascript
function getDesc (obj, prop) {
  var desc = Object.getOwnPropertyDescriptor(obj, prop);
  return desc || (obj=Object.getPrototypeOf(obj) ? getDesc(obj, prop) : void 0);
}
function multiInherit (...protos) {
  return Object.create(new Proxy(Object.create(null), {
    has: (target, prop) => protos.some(obj => prop in obj),
    get (target, prop, receiver) {
      var obj = protos.find(obj => prop in obj);
      return obj ? Reflect.get(obj, prop, receiver) : void 0;
    },
    set (target, prop, value, receiver) {
      var obj = protos.find(obj => prop in obj);
      return Reflect.set(obj || Object.create(null), prop, value, receiver);
    },
    *enumerate (target) { yield* this.ownKeys(target); },
    ownKeys(target) {
      var hash = Object.create(null);
      for(var obj of protos) for(var p in obj) if(!hash[p]) hash[p] = true;
      return Object.getOwnPropertyNames(hash);
    },
    getOwnPropertyDescriptor(target, prop) {
      var obj = protos.find(obj => prop in obj);
      var desc = obj ? getDesc(obj, prop) : void 0;
      if(desc) desc.configurable = true;
      return desc;
    },
    preventExtensions: (target) => false,
    defineProperty: (target, prop, desc) => false,
  }));
}
```
[More on stackoverflow](https://stackoverflow.com/questions/9163341/multiple-inheritance-prototypes-in-javascript)


# Temporal dead zone
`let` and `const` are hoisted (like `var`, `class` and `function`), but there is a period between entering scope and being declared where they cannot be accessed. This period is the **temporal dead zone (TDZ)**.
```javascript
let foo = () => bar; 
let bar = 'bar'; 
foo();
```
[ECMA-262 Standard](https://262.ecma-international.org/9.0/#sec-let-and-const-declarations): let and const declarations define variables that are scoped to the running execution context's LexicalEnvironment. The variables are created when their containing Lexical Environment is instantiated but may not be accessed in any way until the variable's LexicalBinding is evaluated.


# What's a typical use case for anonymous functions?
Since Anonymous Functions are function expressions rather than the regular function declaration which are statements. Function expressions are more flexible. We can assign functions to variables, object properties, pass them as arguments to other functions, and even write a simple one line code enclosed in an anonymous functions.
- Function expressions
- IIFE
- Callback functions
- Returning function from another function