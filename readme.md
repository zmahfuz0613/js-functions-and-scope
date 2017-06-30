# Functions and Scope

We've learned a lot of things that are fundamental to programming, such as primitive and complex data types, conditionals, and loops. However, we still need a way to encapsulate logic and make it reusable (make our code more DRY). Functions are a fundamental part of JavaScript that allow us to contain all of the logic of a particular operation within a named entity that can be activated, or "called", repeatedly from other parts of our code.

One feature of functions in JavaScript is that each function creates a new "scope" when it is defined. Scope defines what variables and functions are accessible at any given point in the execution of your code. Understanding scope in JavaScript is key to writing bulletproof code and being a better developer.

Chances are, you'll be asked about it during technical interviews too.


## Learning Objectives

### Functions
- Describe what a JavaScript function is
- Recognize the parts of a function
- Write a function in JavaScript using a declaration and an expression
- State the difference between a function's output and side effects
- Differentiate between referencing and invoking a function
- Define hoisting

### Scope
- Describe scope and how it governs how data is able to be accessed in code
- Give an example of a function declaration and a function expression
- Describe the impact of hoisting on variable scope



## Functions

**What is a Function?**

* Fundamental component of JavaScript
* A reusable block of JavaScript code
* Simply put, a function is a block of code that takes an input, processes that input and then produces some form of output

---

**Why do we use functions?**
Benefits of functions:
* Reusability
* DRYness
* Naming convention (describes intent)

---

### Recognize the Parts (5 minutes / 0:15)

**What are the components of a function?**

#### Function Container

```js
function multiply(){

}
```

#### Input ("Arguments" or "Parameters")

```js
function multiply( num1, num2 ){

}
```

#### Output and Side Effects

```js
function multiply( num1, num2 ){
  console.log( num1 * num2 )
  return num1 * num2
}
```
* Output: What the function returns (evaluates to)
* Side Effects: Effects the function has on data outside of itself (external to its scope)

**Q: Does a function need an input, output and/or side effects to work?**

> Short answer: No, a function may have any combination of these.  
> Note: If you don't specify an return value, it will return `undefined`.

### Calling and Referencing a Function (5 minutes / 0:20)

We've defined a function. Now we need to call it...

**Q: Now we that we have stored that function in memory, how to do we use it?**

```js
// Call the multiply function.
multiply( 2, 5 )

// What happens if we reference the function without parentheses?
multiply
```

### You do - Create a Function (5 minutes / 0:25)
It would be really nice if there was a function that did exponents for us. Create a `square` function, it should:

- Take an argument that is a number
- The function's output should return the number squared

```js
square(4)
=> 16
```

**Bonus - Create an exponents function**
- it should take 2 arguments
  - the first should be the base number
  - the second should be the power you'd like to raise the base number to

It should look something like this:

```js
raisePower(4, 3)
=> 64
```

### Function Declarations and Expressions (10 minutes / 0:35)

There are two ways to define a function...

#### Declaration

``` javascript
function multiply( num1, num2 ) {
  return num1 * num2
}
```

#### Expression

``` javascript
var multiply = function ( num1, num2 ) {
  return num1 * num2
}
```

#### Declarations vs. Expressions

Both do the same thing and run the same chunk of code but they are different.

**Q. What differences do you notice?**

- **Function declarations** define functions without assigning them to variables.
- **Function expressions** assign *anonymous functions* to variables.


While we call/reference functions defined through declarations and expressions the same way, they do have a subtle but important difference...

### Hoisting (10 minutes / 0:45)

Function declarations are processed before any code is executed, meaning you can call functions before they are declared in the flow of your code. This behavior is known as **hoisting**.

Conversely, function expressions **are not** hoisted, meaning you cannot call them before they are defined in the flow of your code.

What do you think will happen when we run the below code...
```js
multiply( 3, 5 )
var multiply = function( num1, num2 ){
  return num1 * num2
}
// function expression
```

Surely the same thing will happen when we run the below code...

```js
multiply( 3, 5 )
function multiply( num1, num2 ) {
  return num1 * num2
}
// function declaration
```
> We can successfully call the multiply function before declaring it. When our script file loads, the browser processes all function declarations first, and then runs the rest of our JavaScript from top to bottom.

Knowing this, what will happen each time we call `express` and `declare` in the below example?

```js
express()        // What happens when we run this function at this point in the code?

var express = function() {
    console.log('Function expression called.')
}
```

What changes when we run?

```js
var express = function() {
    console.log('Function expression called.')
}

declare()        // ???
express()        // ???

function declare() {
    console.log('Function declaration called.')
}
```

### ES6 Features (10 minutes / 0:55)

#### Arrow Functions

Following the release of ECMAScript 6 (ES6) in 2016, anonymous functions can be written as "arrow functions", a syntax adapted from CoffeeScript.
```js
var multiply = function( num1, num2 ){  // function expression
  return num1 * num2
}

multiply( 3, 5 )
```

What does this look like in ES6?
```js
const multiply = (num1, num2) => {
  return num1 * num2
}
```

Or, to simplify it further..

```js
const multiply = (num1, num2) => num1 * num2
```
Arrow functions with a "concise" function body (no brackets and on one line) have "implicit return" (no return statement necessary)

However, this single line return can be faked with parentheses
```js
const multiply = (num1, num2) => (
  num1 * num2
)
```

#### Optional Parameters

A second feature introduced by ES6 was optional function parameters. Optional parameters allow us to define parameters that will default to some pre-determined value if the function is called without passing them in. We can set optional parameters in a function definition by assigning a value to the parameter definition.

```js
function exponentiate(base, exponent = 2) {
  return base ** exponent
}

exponentiate(4, 3)
=> 64

exponentiate(4)
=> 16
```
> Optional parameters are very useful when writing **recursive** functions as they allow values to more easily be passed through multiple function calls

## Exercise: Fun with Functions Quiz (15 minutes / 1:10)
> 10 minutes exercise, 5 minutes review

What is alerted in each case? Write down your answer before running the code.

1.
```js
function foo(){
  function bar() {
      return 3
  }
  return bar()
  function bar() {
      return 8
  }
}
alert(foo())
```
2.
```js
function foo(){
  var bar = function() {
      return 3
  }
  return bar()
  var bar = function() {
      return 8
  }
}
alert(foo())
```

3.
```js
function foo(){
  return bar()
  var bar = function() {
      return 3
  }
  var bar = function() {
      return 8
  }
}
alert(foo())
```

4.
```js
function foo(){
  var bar = () => {
      return 3
  }
  return bar()
  var bar = () => {
      return 8
  }
}
alert(foo())
```

5.
```js
function foo(){
  var bar = () => 3
  return bar()
  var bar = () => 8
}
alert(foo())
```

6.
```js
function foo(){
  var bar = () => { 3 }
  return bar()
  var bar = () => { 8 }
}
alert(foo())
```
> NOTE: For an arrow function to have implicit return, it **cannot** have a block body enclosed with brackets `{` `}`

**Hungry for More?**

> Grab a Snickers || Try implementing [fizzBuzz](https://github.com/ga-wdi-exercises/fizzBuzz_redux) with Functions!

### Break (10 minutes / 1:15)
