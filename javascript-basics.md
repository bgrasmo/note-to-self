# Learning JavaScript - the basics
Documenting what I learn about Javascript as I go, to keep as a reference-guide for myself as I am sure to need it.

# Variables
Three different ways to declare a variable in Javascript:
```javascript
var var1 = 'Some';
let var2 = 'String';
const var3 = 'Here';
```
Var is scoped globally or to the function it was defined, while let and const are scoped to the function or block they are defined in.

Scope defines the rules for the visibility of variables. A brief example with global scope:
```javascript
// Variables defined in the root/bottom will be available globally
var var1 = 'Some';
let var2 = 'String';
const var3 = 'Here';

function consoleIt () {
    console.log(var1);
    console.log(var2);
    console.log(var3);
}
consoleIt(); // Prints the 3 global variables
```
A brief example with function scope:
```javascript
function defineIt() {
    var var1 = 'Some';
    let var2 = 'String';
    const var3 = 'Here';
}
console.log(var1);
console.log(var2);
console.log(var3);
// Fails because they are defined in function and only available in the function, not globally
```

A brief example with block scope:
```javascript
if (true) {
    var var1 = 'Some';
    let var2 = 'String';
    const var3 = 'Here';
}
console.log(var1);
console.log(var2);
console.log(var3);
// Only var1 is printed because it is var, and defined globally unless inside a function.
```
In short, don't use var but use let or const instead. More about that later.

Var and let can be redefined, const can't as it is immutable:
```javascript
// Define the variables first
var var1 = 'Some';
let var2 = 'String';
const var3 = 'Here';

// Now assign new values to them
var1 = 'New';
var2 = 'Text';
var3 = 'Added';
// The first two works, the last doesn't
```

# Data types
Variables can be of different types

```javascript
// String:
let name = 'Your name here';

// Number:
let a = -1;
let b = 0;
let c = 1000000;
let pi = 3.14;

// Boolean:
let on = true;
let off = false;

// Object:
let person = {
    firstName: 'Some',
    lastName: 'Name',
    age: 31
};

// Objects can be nested:
let household = {
    firstName: 'Someone',
    lastName: 'Else',
    age: 57,
    address: {
        streetName: '21 st',
        city: 'New York',
        country: 'USA'
    }
};

// Undefined, not yet declared, or declared but not assigned a value:
let timezone;

// Null, declared and has been assgined a value, but value is currently empty
let nothing = null;
```

function ```typeof``` can be used to find what type a variable is:
```javascript
let name = 'Your name here';
let b = 0;
let on = true;
let person = {
    firstName: 'Some',
    lastName: 'Name',
    age: 31
};
console.log(typeof name);   // string
console.log(typeof b);      // number
console.log(typeof on);     // boolean
console.log(typeof person); // object
```

# Basic math
Some basic math operations
```javascript
// add
let a = 10 + 1; // 11

// subtract
let b = 10 - 5; // 5

// divide
let c = 20 / 2; // 10

// multiply
let d = 10 * 2; // 20
```
If the variables already contains a value, they can be added to or subtracted from like this:
```javascript
// Increment a by 1
a = a + 1;

// Or more briefly like this:
a += 1;

// Or even just this:
a++;

// replace + with - to subtract instead
b -= 1;
b--;

// Divide can be shortened like this:
c /= 2; // Divides the value of c by 2

// Multiply:
d *= 2; // Multiplies the value of d by 2
```

For adding and subtracting, you can either do the add or subtract before the operation, or after:
```javascript
let a = 10;
console.log(a++); // prints 10, then adds 1 to a
console.log(a); // Now it is 11

let b = 20;
console.log(++b); // adds 1 to a, then prints so result is 21
console.log(b); // Still 21
```
# The math library
Javascript has a math library built in with more useful functions. Search for ```mdn javascript math``` for the documentation: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math

```javascript
// Find the smallest value
let smallest = Math.min(3, 8, 2, 7); // 2

// Find the largest value
let largest = Math.max(3, 8, 2, 7); // 8

// Round value down
let floor = Math.floor(1.9); // 1

// Round value up
let ceil = Math.ceil(1.9); // 2

// This can be nested, find the largest value and round it up
let maxCeil = Math.ceil(Math.max(0.1, 1.7, 5.3, 2.8)); // 5.3 is max, ceil rounds it up to 6
```