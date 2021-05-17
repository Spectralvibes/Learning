
# Find unique elements in an Array:
Using Set and Spread:
```javascript
var a = [1, 1, 2];

[... new Set(a)]
```
Using Filter and indexOf:
```javascript
list = list.filter((currentItem, index, array) => array.indexOf(currentItem) === index)
```
Example that uses no libraries: this requires two new prototype functions, contains and unique:
```javascript
Array.prototype.contains = function(v) {
  for (var i = 0; i < this.length; i++) {
    if (this[i] === v) return true;
  }
  return false;
};
Array.prototype.unique = function() {
  var arr = [];
  for (var i = 0; i < this.length; i++) {
    if (!arr.contains(this[i])) {
      arr.push(this[i]);
    }
  }
  return arr;
}
var duplicates = [1, 3, 4, 2, 1, 2, 3, 8];
var uniques = duplicates.unique(); // result = [1,3,4,2,8]
console.log(uniques);
```


# Output?
```javascript
var x = 23;

(function(){
var x = 43;
(function random(){
x++;
console.log(x);
var x = 21;
})();
})();
```
`NaN` // Due to hoisting within IIFE


# Output?
```javascript
var obj1 = {
  valueOfThis: function(){
    return this;
  }
}

var obj2 = {
  valueOfThis: ()=>{
    return this;
  }
}
```


# How to write a recursive function?


# What is the value of foo?
var foo = 10 + '20';


# Question: What will be the output of the code below?
console.log(0.1 + 0.2 == 0.3);


# Question: How would you make this work?
add(2, 5); // 7
add(2)(5); // 7


# Question: What value is returned from the following statement?
"i'm a lasagna hog".split("").reverse().join("");
Question: What is the value of window.foo?
( window.foo || ( window.foo = "bar" ) );


# Question: What is the outcome of the two alerts below?
var foo = "Hello";
(function() {
  var bar = " World";
  alert(foo + bar);
})();
alert(foo + bar);


# Question: What is the value of foo.length?
var foo = [];
foo.push(1);
foo.push(2);


# Question: What is the value of foo.x?
var foo = {n: 1};
var bar = foo;
foo.x = foo = {n: 2};


# Question: What does the following code print?
console.log('one');
setTimeout(function() {
  console.log('two');
}, 0);
console.log('three');


# How to Flatten a Nested Javascript Array arr = [1,[1,2],[1,2,3]]
```javascript
let arr = [[1, 2],[3, 4],[5, 6, 7, 8, 9],[10, 11, 12]];
// Expected output
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
```
> concat() and apply()
```javascript
[].concat.apply([], arr);
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 ]
```
> 
>Using methods
```javascript
arr.join();
// Output: "1,1,2,1,2,3" 
arr.flat();
//Output: [1, 1, 2, 1, 2, 3]
```
>Without direct methods
```javascript
arr.forEach(element => {
    if (typeof element === 'object') {
        element.forEach(nestedElement => {
            console.log(nestedElement);
        });
    } else {
        console.log(element);
    }
})
```
[Different ways](https://codeburst.io/how-to-flatten-a-nested-javascript-array-628e01b85512)
[Array.prototype.flat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)
[Array.prototype.flat() polyfill](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)(https://github.com/behnammodi/polyfill/blob/master/array.polyfill.js)


# Output?
```javascript
a = b;
b = 5;
// 
let a = b;
var b = 5;
```