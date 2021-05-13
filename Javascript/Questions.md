# What is JavaScript?
JavaScript (JS) is a lightweight interpreted or JIT-compiled programming language with first-class functions.



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
[More on let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
[More on const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
[More on var](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)


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
[ECMA specification](https://262.ecma-international.org/6.0/#sec-createperiterationenvironment)
[Stackoverflow answer](https://stackoverflow.com/questions/30899612/explanation-of-let-and-block-scoping-with-for-loops)

# What is ‘this’ keyword in JavaScript?
>The `this` keyword refers to the function's execution context. `this` evaluates to the value of the ThisBinding of the current execution context
It has different values depending on where it is used:
- In a method, this refers to the owner object.
- Alone, this refers to the global object.
- In a function, this refers to the global object.
- In a function, in strict mode, this is undefined.
- In an event, this refers to the element that received the event.
- Methods like call(), and apply() can refer this to any object paased as an argument.
[More on MDN...](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
[More on W3Schools...](https://www.w3schools.com/js/js_this.asp)


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
[David Walsh blog](https://davidwalsh.name/event-delegate)
[Dmitri Pavlutin blog](https://dmitripavlutin.com/javascript-event-delegation/)


# Events in detail
[More on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)


# Explain how prototypal inheritance works?
JavaScript objects are dynamic "bags" of properties (referred to as own properties). JavaScript objects have a link to a prototype object. When trying to access a property of an object, the property will not only be sought on the object but on the prototype of the object, the prototype of the prototype, and so on until either a property with a matching name is found or the end of the prototype chain is reached.
[Know more...](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#inheritance_with_the_prototype_chain)
[Why prototypical inheritance matters](http://aaditmshah.github.io/why-prototypal-inheritance-matters/)


# Different ways to create objects and the resulting prototype chain:
[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#different_ways_to_create_objects_and_the_resulting_prototype_chain)


# How Pseudoclassical Inheritance works?
[Pseudoclassical Inheritance](https://dev.to/tangweejieleslie/pseudoclassical-inheritance-pattern-in-javascript-1a48)


# What is a closure, and how/why would you use one?
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
[Know more...](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)


# Function in detail
[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)


# Generators:
Generators are functions that can be exited and later re-entered. Their context (variable bindings) will be saved across re-entrances.
- **Generator function***: The function* declaration (function keyword followed by an asterisk) defines a generator function, which returns a Generator object.
[Generator function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)
- **Generator object**: The Generator object is returned by a generator function and it conforms to both the iterable protocol and the iterator protocol.
[Generator object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator)


# What are async functions?
An async function is a function declared with the async keyword, and the await keyword is permitted within them. The async and await keywords enable asynchronous, promise-based behavior to be written in a cleaner style, avoiding the need to explicitly configure promise chains.
[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)


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


# function types
- First class functions:
A programming language is said to have First-class functions when functions in that language are treated like any other variable. For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable.
- Higher order function:
A function that returns a function is called a Higher-Order Function.
- Pure functions
The function return values are identical for identical arguments.

# Nested functions and closures
You may nest a function within another function. The nested (inner) function is private to its containing (outer) function.

It also forms a closure. A closure is an expression (most commonly, a function) that can have free variables together with an environment that binds those variables (that "closes" the expression).

Since a nested function is a closure, this means that a nested function can "inherit" the arguments and variables of its containing function. In other words, the inner function contains the scope of the outer function.
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#nested_functions_and_closures)


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


# 46.	Identifiers
# 47.	Literals
# 48.	Primitive types & objects
# 49.	Numbers=> Math
# 50.	Strings
# 51.	Special characters
# 52.	Booleans
# 53.	Symbols
# 54.	Regular expressions
# 55.	Objects
# 56.	Number,String,Booolean Objects
# 57.	Trailing commas in Objects n Arrays
# 58.	Dates
# 59.	Maps & Sets
# 60.	Data type conversion/Coersion
# 61.Control flow statements and flow patterns
# 62.Expressions and Operators
# 63.Destructuring
# 67.	Pass by value n pass by reference
# 69.	Arrow notation
# 71. Scope:
# 72.	Lexical vs dynamic scope
# 73.	Global/block scope
# 74.	Variable masking
# 76.	IIFE
# 77.	Functions n hoisting
# 78.	Temporal dead zone
# 80. Arrays: 
# 81.	Methods
# 82.	manipulation techniques
# 85.	Multiple inheritance
# 86.	Mixin
# 87. interface
# 88. Maps & Sets
# 89. Exceptions & error handling
# 90. Events:
# 91. Async programming
# 92. Callbacks
# 93. Promises
# 96. Ajax & JQuery
# 97. valueof and unboxing
# 98. How to find memory leaks in JavaScript?
# 99. JavaScript memory management
# 100. Applications caching
# 101. Service worker

# 32.What are the pros and cons of using Promises instead of callbacks?
# 33.What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?
# 34.What tools and techniques do you use debugging JavaScript code?
# 35.What language constructions do you use for iterating over object properties and array items?
# 36.Explain the difference between mutable and immutable objects.
# 37.Explain the difference between synchronous and asynchronous functions.
# 38.What is event loop? What is the difference between call stack and task queue?
# 40. What is MonkeyPatching?


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


# 12.Difference between: function Person(){}, var person = Person(), and var person = new Person()?


# 11.What's the difference between host objects and native objects?


# What do you think of AMD vs CommonJS?


# What's the difference between a variable that is: null, undefined or undeclared?


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


# What's a typical use case for anonymous functions?
- Function expressions
- IIFE
- Callback functions
- Returning function from another function