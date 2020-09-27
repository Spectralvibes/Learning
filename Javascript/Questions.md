# Interview Questions

## 1.What is JavaScript?
JavaScript (JS) is a lightweight interpreted or JIT-compiled programming language with first-class functions.

## 2.What are JavaScript data types?
In JavaScript, a primitive (primitive value, primitive data type) is data that is not an object and has no methods. There are 6 primitive data types: string, number, boolean, null, undefined, symbol (new in ECMAScript 2015).

All primitives are immutable, i.e., they cannot be altered. It is important not to confuse a primitive itself with a variable assigned a primitive value. The variable may be reassigned a new value, but the existing value can not be changed in the ways that objects, arrays, and functions can be altered.

Except for null and undefined, all primitive values have object equivalents that wrap around the primitive values:

* `String` for the string primitive.
* `Number` for the number primitive.
* `Boolean` for the boolean primitive.
* `Symbol` for the symbol primitive.

The wrapper's valueOf() method returns the primitive value.

```javascript
Number(6).valueof()
// 6
```
  Data type | 	Description
  --------- | 	------------------------------
  String  	|	In any computer programming language, a string is a sequence of characters used to represent text. In JavaScript, a String is one of the primitive values and the String object is a wrapper around a String primitive.
  Number  	|	In JavaScript, Number is a numeric data type in the double-precision 64-bit floating point format (IEEE 754). In other programming languages different numeric types can exist, for examples: Integers, Floats, Doubles, or Bignums.
  Boolean	|	Boolean represents a logical entity and can have two values: true, and false (Sepcial keywords in JS).  The Boolean value is named after English mathematician George Boole, who pioneered the field of mathematical logic.
  Symbol	|	Symbols are completely unique identifiers. Just like their primitive counterparts (Number, String, Boolean), they can be created using the factory function Symbol() which returns a Symbol. A symbol value may be used as an identifier for object properties; this is the data type's only purpose. [More...](https://medium.freecodecamp.org/how-did-i-miss-javascript-symbols-c1f1c0e1874a)
  null    | In computer science, a null value represents a reference that points, generally intentionally, to a nonexistent or invalid object or address. In javascript, the value null represents the intentional absence of any object value. The Null type has exactly one value: `null`. 
  undefined | The global undefined property represents the primitive value undefined. A variable that has not been assigned a value has the value `undefined`. 
  Array		|	Arrays are list-like objects whose prototype has methods to perform traversal and mutation operations.
  Object	|	In computer science, an object is a value in memory which is possibly referenced by an identifier. In JavaScript, objects can be seen as a collection of properties. Basically, anything. Everything in JavaScript is an object, and can be stored in a variable.
  
  [More details...](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)

## 3.What is ‘this’ keyword in JavaScript?


>The `this` keyword refers to the function's execution context.
`this` evaluates to the value of the ThisBinding of the current execution context


“this” inside of an event handler always refers to the element it was triggered on.

In most cases, the value of this is determined by how a function is called. It can't be set by assignment during execution, and it may be different each time the function is called. ES5 introduced the bind method to set the value of a function's this regardless of how it's called, and ES6 introduced arrow functions whose this is lexically scoped (it is set to the this value of the enclosing execution context).  
  

Global context:
In the global execution context (outside of any function),  `this`  refers to the global object, whether in strict mode or not.  
  
Function context
Inside a function, the value of  `this`  depends on how the function is called.  

-   Simple call:
Since the following code is  `not in strict mode`, and because the value of this is not set by the call, this will default to the global object:

```javascript
1.  function f1(){
2.  return this;
3.  }
4.  // In a browser:
5.  f1() === window; // the window is the global object in browsers
6.  // In Node:
7.  f1() === global
```

In  `strict mode`, however, the value of this remains at whatever it was set to when entering the execution context, so, in the following case, this will default to undefined:

```Javascript
1.  function f2(){
2.    "use strict"; // see strict mode
3.    return this;
4.  }
5.  f2() === undefined;
```
So, in strict mode, if this was not defined by the execution context, it remains `undefined`.

Prior to ECMA 5,  `this`  in the inner function would refer to the global window object; whereas, as of ECMA 5,  `this`  in the inner function would be undefined.
```javascript
1.  var myObject = {
2.   foo: "bar",
3.   func: function() {
4.      var self = this;
5.      console.log("outer func:  this.foo = " + this.foo);
6.      console.log("outer func:  self.foo = " + self.foo);
7.      (function() {
8.          console.log("inner func:  this.foo = " + this.foo);
9.          console.log("inner func:  self.foo = " + self.foo);
10.      }());
11.    }
12.  };
13.  myObject.func();
```
Output:
>-   outer func:  this.foo = bar
>-   outer func:  self.foo = bar
>-   inner func:  this.foo = undefined
>-   inner func:  self.foo = bar

**call and apply**
The  **call()**  method calls a function with a given  `this`  value and arguments provided individually.

The  **apply()**  method calls a function with a given  `this`  value and  `arguments`  provided as an array (or an  [array-like object](/en-US/docs/Web/JavaScript/Guide/Indexed_collections#Working_with_array-like_objects)).

> **Note**: While the syntax of this function is almost identical to that of call(), the fundamental difference is that call() accepts an argument list, while apply() accepts a single array of arguments.
```javascript
1.  function add(c, d){
2.    return this.a + this.b + c + d;
3.  }
5.  var o = {a:1, b:3};
7.  // The first parameter is the object to use as
8.  // 'this', subsequent parameters are passed as 
9.  // arguments in the function call
10.  add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16
12.  // The first parameter is the object to use as
13.  // 'this', the second is an array whose
14.  // members are used as the arguments in the function call
15.  add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34
```

**The bind method**
The  **bind()**  method creates a new function that, when called, has its  `this`  keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

The.bind() method is used to permanently set the value of this inside the target function to the passed in context object.
```javascript
1.  function f(){
2.    return this.a;
3.  }
4.  var g = f.bind({a:"azerty"});
5.  console.log(g()); // azerty
6. 
7.  var h = g.bind({a:"yoo"}); // bind only works once!
8.  console.log(h()); // azerty
9.
10. var o = {a:37, f:f, g:g, h:h};
11.  console.log(o.f(), o.g(), o.h()); // 37, azerty, azerty
```

The  **bind()**  function creates a new  **bound function**  **(BF)**. A  BF  is an  **exotic function object**  (a term from  ECMAScript 2015) that wraps the original function object. Calling a  BF  generally, results in the execution of its  **wrapped function**.  
A  BF  has the following internal properties:

-   **[[BoundTargetFunction]]** - the wrapped function object;
-   **[[BoundThis]]**  - the value that is always passed as  **this**  value when calling the wrapped function.
-   **[[BoundArguments]]**  - a list of values whose elements are used as the first arguments to any call to the wrapped function.
-   **[[Call]]**  - executes code associated with this object. Invoked via a function call expression. The arguments to the internal method are a  **this**  value and a list containing the arguments passed to the function by a call expression.

When bound function is called, it calls internal method **[[Call]]**  with following arguments  **Call(_target_,  _boundThis_,  _args_).**  Where,  **_target_**  is **[[BoundTargetFunction]]**,  **_boundThis_** is  **[[BoundThis]]**,  _**args**_ is  **[[BoundArguments]]**.

A bound function may also be constructed using the  [`new`](/en-US/docs/Web/JavaScript/Reference/Operators/new "The new operator creates an instance of a user-defined object type or of one of the built-in object types that has a constructor function.")  operator: doing so acts as though the target function had instead been constructed. The provided  **`this`**  value is ignored, while prepended arguments are provided to the emulated function.

  

**Arrow functions**

An  **arrow function expression**  has a shorter syntax than a [function expression](/en-US/docs/Web/JavaScript/Reference/Operators/function) and does not bind its own [this](/en-US/docs/Web/JavaScript/Reference/Operators/this), [arguments](/en-US/docs/Web/JavaScript/Reference/Functions/arguments), [super](/en-US/docs/Web/JavaScript/Reference/Operators/super), or [new.target](/en-US/docs/Web/JavaScript/Reference/Operators/new.target). Arrow functions are always  [anonymous](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/name). These function expressions are best suited for non-method functions, and they cannot be used as constructors.

There is one subtle difference in behavior between ordinary  `function`  functions and arrow functions.  **Arrow functions do not have their own  `this`  value.**  The value of  `this`  inside an arrow function is always inherited from the enclosing scope.
```javascript
1.  (param1, param2, …, paramN) => { statements }
2.  (param1, param2, …, paramN) => expression
3.  // equivalent to: (param1, param2, …, paramN) => { return expression; }

5.  // Parentheses are optional when there's only one parameter:
6.  (singleParam) => { statements }
7.  singleParam => { statements }

9.  // A function with no parameters requires parentheses:
10.  () => { statements }
11.  () => expression // equivalent to: () => { return expression; }
```
**Object method**
When a function is called as a method of an object, its  `this`  is set to the object the method is called on.
In the following example, when  `o.f()`  is invoked, inside the function  `this`  is bound to the  `o`  object.
```javascript
1.  var o = {
2.    prop: 37,
3.    f: function() {
4.      return this.prop;
5.    }
6.  };

8.  console.log(o.f()); // logs 37
```

**As a constructor**:
When a function is used as a constructor (with the  [new](/en-US/docs/Web/JavaScript/Reference/Operators/new)  keyword), its  `this`  is bound to the new object being constructed.

**As a DOM event handler**:
When a function is used as an event handler, its  `this`  is set to the element the event fired from (some browsers do not follow this convention for listeners added dynamically with methods other than  `addEventListener`).

## 4.What is map and reduce in JavaScript?

## 5.Explain event delegation
## 6.Explain how prototypal inheritance works? How Pseudoclassical Inheritance works?
## 7.What do you think of AMD vs CommonJS?
## 8.What's the difference between a variable that is: null, undefined or undeclared?
## 9. What is a closure, and how/why would you use one?
## 10. What's a typical use case for anonymous functions?
## 11.What's the difference between host objects and native objects?
## 12.Difference between: function Person(){}, var person = Person(), and var person = new Person()?
## 13.What's the difference between .call and .apply?
## 14.Explain Function.prototype.bind.
## 15.When would you use document.write()?
## 16.What's the difference between feature detection, feature inference, and using the UA string?
## 17.Explain Ajax in as much detail as possible.
## 18.Explain how JSONP works (and how it's not really Ajax).
## 19.Have you ever used JavaScript templating?
## 20.Explain "hoisting".
## 21.Describe event bubbling.
## 22.What's the difference between an "attribute" and a "property"?
## 23.Why is extending built-in JavaScript objects not a good idea?
## 24.Difference between document load event and document DOMContentLoaded event?
## 25.Explain the same-origin policy with regards to JavaScript.
## 26.Why is it called a Ternary expression, what does the word "Ternary" indicate?
## 27.What is "use strict";? what are the advantages and disadvantages to using it? What is lint?
## 28.Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?
## 29.Why would you use something like the load event? Does this event have disadvantages? Do you know any alternatives, and why would you use those?
## 31.What is the extent of your experience with Promises and/or their polyfills?
## 32.What are the pros and cons of using Promises instead of callbacks?
## 33.What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?
## 34.What tools and techniques do you use debugging JavaScript code?
## 35.What language constructions do you use for iterating over object properties and array items?
## 36.Explain the difference between mutable and immutable objects.
## What is an example of an immutable object in JavaScript?
## What are the pros and cons of immutability?
## How can you achieve immutability in your own code?
## 37.Explain the difference between synchronous and asynchronous functions.
## 38.What is event loop? What is the difference between call stack and task queue?
## 39.What are the differences between variables created using let, var or const?
## 40. What is MonkeyPatching?
## 41.What is higher order function?
## 42. What are ES6 features?
## 43. Prototype chain
## 44.Datatypes:
## 45.	Variables and constants & which to use
## 46.	Identifiers
## 47.	Literals
## 48.	Primitive types & objects
## 49.	Numbers=> Math
## 50.	Strings
## 51.	Special characters
## 52.	Booleans
## 53.	Symbols
## 54.	Regular expressions
## 55.	Objects
## 56.	Number,String,Booolean Objects
## 57.	Trailing commas in Objects n Arrays
## 58.	Dates
## 59.	Maps & Sets
## 60.	Data type conversion/Coersion
## 61.Control flow statements and flow patterns
## 62.Expressions and Operators
## 63.Destructuring
## 64.Functions:
## 65.	First class functions
## 66.	Closures
## 67.	Pass by value n pass by reference
## 68.	this keyword reference
## 69.	Arrow notation
## 70.	Call, apply and Bind
## 71.Scope:
## 72.	Lexical vs dynamic scope
## 73.	Global/block scope
## 74.	Variable masking
## 75.	Functions, closures and lexical scope
## 76.	IIFE
## 77.	Functions n hoisting
## 78.	Temporal dead zone
## 79.	Strict mode
## 80.Arrays: 
## 81.	Methods
## 82.	manipulation techniques
## 83.Objects:
## 84.	Prototypal chain & Inheritance
## 85.	Multiple inheritance
## 86.	Mixin
## 87. interface
## 88. Maps & Sets
## 89. Exceptions & error handling
## 90. Events:
## 91. Async programming
## 92. Callbacks
## 93. Promises
## 94. Generators
## 95. Event delegation
## 96. Ajax & JQuery
## 97. valueof and unboxing
## 98. How to find memory leaks in JavaScript?
## 99. JavaScript memory management
## 100. Applications caching
## 101. Service worker
## 102. 
## 103.
## 104.
## 105.
## 106.
## 107.
## 108.
## 109.



Performance Questions:

## What tools would you use to find a performance bug in your code?
##  What are some ways you may improve your website's scrolling performance?
## Explain the difference between layout, painting and compositing.


Network Questions:
## Traditionally, why has it been better to serve site assets from multiple domains?
## What are the differences between Long-Polling, Websockets and Server-Sent Events?
## Do your best to describe the process from the time you type in a website's URL to it finishing loading on your screen.
## Explain the following request and response headers:
## Diff. between Expires, Date, Age and If-Modified-...
## Do Not Track
## Cache-Control
## Transfer-Encoding
## ETag
## X-Frame-Options
## What are HTTP methods? List all HTTP methods that you know, and explain them.

# References:
## 1. Primitives: 
https://javascriptweblog.wordpress.com/2010/09/27/the-secret-life-of-javascript-primitives/
## 2. Memory Heap or stack: 
https://hashnode.com/post/does-javascript-use-stack-or-heap-for-memory-allocation-or-both-cj5jl90xl01nh1twuv8ug0bjk
## 3. Stack size:
https://glebbahmutov.com/blog/javascript-stack-size/
## 4. Memory management:
https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec
## 5. Performance tuning:
https://medium.com/@spp020/44-quick-tips-to-fine-tune-angular-performance-9f5768f5d945
## 6. Code review:
https://www.evoketechnologies.com/blog/code-review-checklist-perform-effective-code-reviews/
https://gist.github.com/blakewest/10049924
## 7. Interview questions:
https://www.code-sample.com/2018/04/angular-7-interview-questions-and.html?m=1
## 8. Time saving tips: 
https://blog.angularindepth.com/beware-angular-can-steal-your-time-41fe589483df



Coding Questions:

## What is the value of foo?

var foo = 10 + '20';

## Question: What will be the output of the code below?

console.log(0.1 + 0.2 == 0.3);

## Question: How would you make this work?

add(2, 5); // 7
add(2)(5); // 7

## Question: What value is returned from the following statement?

"i'm a lasagna hog".split("").reverse().join("");
Question: What is the value of window.foo?
( window.foo || ( window.foo = "bar" ) );

## Question: What is the outcome of the two alerts below?

var foo = "Hello";
(function() {
  var bar = " World";
  alert(foo + bar);
})();
alert(foo + bar);

## Question: What is the value of foo.length?

var foo = [];
foo.push(1);
foo.push(2);

## Question: What is the value of foo.x?

var foo = {n: 1};
var bar = foo;
foo.x = foo = {n: 2};

## Question: What does the following code print?

console.log('one');
setTimeout(function() {
  console.log('two');
}, 0);
console.log('three');
