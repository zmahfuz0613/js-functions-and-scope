# Functions and Scope

## Framing (10 min / 10:10)

We've learned a lot of things that are fundamental to programming, such as primitive and complex data types, conditionals, and loops. However, we still need a way to encapsulate logic and make it reusable (make our code more DRY). Functions are a fundamental part of JavaScript that allow us to contain all of the logic of a particular operation within a named entity that can be activated, or "called", repeatedly from other parts of our code.

One feature of functions in JavaScript is that each function creates a new "scope" when it is defined. Scope defines what variables and functions are accessible at any given point in the execution of your code. Understanding scope in JavaScript is key to writing well structured code and being a better developer.

There's a good chance you'll be asked about scope during technical interviews too.


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
- Describe the impact of hoisting on variable scope



## Functions

**What is a Function?**

* Fundamental component of JavaScript
* A reusable block of JavaScript code used to perform a task
* Simply put, a function is a block of code that takes an input, processes that input and then produces some form of output

---

**Why do we use functions?**
Benefits of functions:
* Reusability
* DRYness
* Naming convention (describes intent)

---

### Recognize the Parts (10 min / 10:20)

**What are the components of a function?**

#### Function Container

```js
function multiply () {

}
```

#### Input ("Arguments" or "Parameters")

```js
function multiply (num1, num2) {

}
```

#### Output and Side Effects

```js
function multiply (num1, num2) {
  console.log(num1 * num2) // Side Effect
  return num1 * num2 // Output
}
```
* Output: What the function evaluates to - noted by keyword `return`
* Side Effects: Effects the function has on data outside of itself (external to its scope)

**Q: Does a function need an input, output and/or side effects to work?**

> Short answer: No, a function may have any combination of these.  
> Note: If you don't specify an return value, it will return `undefined`.

#### Calling and Referencing a Function 

We've defined a function. Now we need to call it...

**Q: Now we that we have stored that function in memory, how do we use it?**

```js
// Call the multiply function.
multiply(2, 5)

// Reference the function.  What happens if we reference the function without parentheses?
multiply
```

### You do - Create a Function (5 min / 10:25)
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
exponentiate(4, 3)
=> 64
```

### Function Declarations and Expressions (10 min / 10:35)

There are two ways to define a function...

#### Declaration

```js
function multiply (num1, num2) {
  return num1 * num2
}
```

#### Expression

```js
var multiply = function (num1, num2) {
  return num1 * num2
}
```

#### Declarations vs. Expressions

Both do the same thing and run the same chunk of code but they are different.

**Q. What differences do you notice?**

- **Function declarations** define functions without assigning them to variables.
- **Function expressions** assign *anonymous functions* to variables.


While we call/reference functions defined through declarations and expressions the same way, they do have a subtle but important difference...

### Hoisting (10 min / 10:45)

Function declarations are processed before any code is executed, meaning you can call functions before they are declared in the flow of your code. This behavior is known as **hoisting**.

Conversely, function expressions **are not** hoisted, meaning you cannot call them before they are defined in the flow of your code.

What do you think will happen when we run the below code...
```js
multiply(3, 5)
var multiply = function (num1, num2){
  return num1 * num2
}
// function expression
```

Surely the same thing will happen when we run the below code...

```js
multiply(3, 5)
function multiply (num1, num2) {
  return num1 * num2
}
// function declaration
```
> We can successfully call the multiply function before declaring it. When our script file loads, the browser processes all function declarations first, and then runs the rest of our JavaScript from top to bottom.

Knowing this, what will happen each time we call `express` and `declare` in the below example?

```js
express()        // What happens when we run this function at this point in the code?

var express = function () {
  console.log('Function expression called.')
}
```

What about when we run this example?

```js
var express = function () {
  console.log('Function expression called.')
}

declare()        // ???
express()        // ???

function declare () {
  console.log('Function declaration called.')
}
```

You can read more about hoisting [here](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)

### ES6 Features (10 min / 10:55)

#### Arrow Functions

Following the release of ECMAScript 6 (ES6) in 2015, anonymous functions can be written as "arrow functions", a syntax adapted from CoffeeScript.
```js
var multiply = function (num1, num2){  // function expression
  return num1 * num2
}
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
function exponentiate (base, exponent = 2) {
  return base ** exponent
}

exponentiate(4, 3)
=> 64

exponentiate(4)
=> 16
```
> Optional parameters are very useful when writing **recursive** functions as they allow values to more easily be passed through multiple function calls

## Exercise: Fun with Functions Quiz (15 min / 11:10)
> 10 minutes exercise, 5 minutes review

What is alerted in each case? Write down your answer before running the code.

1.
```js
function foo () {
  function bar () {
    return 3
  }

  return bar()

  function bar () {
    return 8
  }
}

alert(foo())
```
2.
```js
function foo () {
  var bar = function () {
    return 3
  }

  return bar()

  var bar = function () {
    return 8
  }
}

alert(foo())
```

3.
```js
function foo () {
  return bar()

  var bar = function () {
    return 3
  }

  var bar = function () {
    return 8
  }
}

alert(foo())
```

4.
```js
function foo () {
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
function foo () {
  var bar = () => 3

  return bar()

  var bar = () => 8
}

alert(foo())
```

6.
```js
function foo () {
  var bar = () => { 3 }

  return bar()

  var bar = () => { 8 }
}

alert(foo())
```
> NOTE: For an arrow function to have implicit return, it **cannot** have a block body enclosed with brackets `{` `}`

<details>
  <summary><em>Answers, try not to peak!</em></summary>
  <p>1.) 8 - 2nd function declaration of `bar` replaces the 1st because of hoisting</p>
  <p>2.) 3 - 1st function expression of `bar` is what is called.  2nd definition is not hoisted</p>
  <p>3.) TypeError - `bar` is called before it is defined by expressions.  Nothing is hoisted</p>
  <p>4.) 3 - Arrow functions count as expressions.  Nothing is hoisted, 1st definition wins.</p>
  <p>5.) 3 - Same as #4, just shorter syntax.</p> 
  <p>6.) Undefined - No return value given, no implicit return.</p>
</details>

--- 

**Hungry for More?**
> Grab a Snickers || Try implementing [FizzBuzz](https://github.com/ga-wdi-exercises/fizzBuzz_redux) with Functions!

## Break (10 min / 11:20)


## Scope

### What Is Scope? (15 min / 11:35)

**In real life:** Your "scope" is what your eyes can see from wherever you're standing.

**In Javascript:** scope is...
* Where a variable can be referenced/used.
* A list of all variables that can be accessed from a given line of code.

> Two ways of saying the same thing.

#### Quick Example

Here's a code snippet that demonstrates some of Javascript's fundamental rules of scope...

```js
function getColor () {
  color = "red"
}

getColor()
console.log(color) // What should we see in the console?
```

Let's see what happens if we add the `var` keyword...

```js
function getAnotherColor () {
  var anotherColor = "green"
}

getAnotherColor()
console.log(anotherColor) // What should we see in the console?
```

#### Rules of Scope in JS

In Javascript, there are two types of scope: **global scope** and **local scope**.

There are four simple rules to remember about scope in JS...

1. Variables created **without** the `var`, `let`, or `const` keywords, no matter where in a program, are placed in the global scope.
2. Variables created **with** the `var`, `let`, or `const` keywords are created in the current local scope.
3. All functions create a new local scope.
4. The current scope includes all outer (enclosing) scopes.

> One consequence of rule 3 is that variables defined outside of any function are inherently global, even if the `var` keyword is used.

![scope diagram](js-es5-scope-2.png)

Another way to say this...

* **Local variables** defined inside a function cannot be accessed from anywhere outside of the function, because the variable is defined only within the scope of the function.
* However, a function can access all variables and functions defined inside the scope in which it is defined (which includes all outer scopes).

### We Do: A More Complex Example (15 min / 11:50)

Let's walk through this example in two steps...
  1. Identify and diagram the scope of each variable.  
  2. Determine whether each `console.log` will error out or not.

```js
teamName = "Giraffes" // What scope is this?
var teamCity = "Sioux Falls" // What scope is this?

function playBaseball () {
  console.log("From " + teamCity + "...") // Does this work?
  console.log("Welcome the " + teamName + "!") // Does this work?

  pitcherName    = "Meg" // What scope is this?
  var batterName = "Perry" // What scope is this?

  console.log(batterName)  // Does this work?
  console.log(pitcherName) // Does this work?
}

playBaseball()

console.log(teamCity) // Does this work?
console.log(teamName)   // Does this work?

console.log(pitcherName) // Does this work?
console.log(batterName)  // Does this work?
```

<details>
  <summary><strong>List of scopes for this example...</strong></summary>

  > `teamName` - global (no var)  
  > `teamCity` - global (not in a function)  
  > `pitcherName` - global (no var)  
  > `batterName` - local to `playBaseball`  

</details>

### More on Hoisting (10 min / 12:00)

#### Functions

A Javascript feature that may impact scope is **hoisting**. This applies to Javascript functions.

Recall that there are two ways to declare functions in Javascript, **function declarations** and **function expressions**.

```js
var sayHello = function () {
    console.log("Hello!")
}

function sayHello () {
    console.log("Hello!")
}
```

#### Hoisting Review

<details>
  <summary>
    Which is a function declaration? Which is a function expression?
  </summary>

  - `var sayHello = function () {}` is a function expression.  
  - `function sayHello () {}` is a function declaration.

</details>

<details>
  <summary>
    How does a function declaration differ from a function expression?
  </summary>

  - A function expression follows the same rules as variable assignment. Since the value of the reference is a function, that function is only available after the assignment.
  - With a function declaration, no matter where you put it in your code, it behaves as if you wrote it as the very first line in your code.
  - Aside from that, they are functionally equivalent.

</details>


#### Variables

Variables are hoisted too, but *their values are not*. More precisely, variable initializations are hoisted, but value assignments are not hoisted.

Variables are first **initialized**, meaning a space in memory is reserved or allocated for the name, but no value is assigned. That variable (or **reference**) will return `undefined` instead of triggering a `ReferenceError`.


```js
console.log("My name is " + firstName)

var firstName = "John"

// My name is undefined
```

### You Do: An Even More Complex Example (15 min / 12:15)

> 10 minutes exercise. 5 minutes review.

In pairs, follow the same process we did in the "We Do" earlier.
  1. Identify and diagram the scope of each variable.  
  2. Determine whether each `console.log` will error out or not.

```javascript
var firstName = 'John' // What scope is this?
var lastName = 'Dowd'  // What scope is this?
var age = 19  // What scope is this?

console.log(displayPerson(firstName, lastName))  // Does this work?
console.log(removeYears()) // Does this work?

function displayPerson (fname, lname) { // What scope are these arguments?
  var prefix = 'Mr'  // What scope is this?
  var fullName = null  // What scope is this?

  function getFullName () {
    var suffix = "Esq."  // What scope is this?
    return fullName = prefix + " " + fname + " " + lname + " " + suffix
  }

  return getFullName()
}

var removeYears = function () {
  var minusYears = 10  // What scope is this?
  var age = 49 // What scope is this?
  return age - minusYears
}
```

### You Do: Test Your Scope Knowledge (15 min / 12:30)

> 10 minutes exercise. 5 minutes review.

Answer the questions below the following code snippet. The letters in the questions and answer choices reference lines in the snippet.

```js
/* A */
var username = "XxXskaterBoi2004XxX"
/* B */
function logIn () {
    /* C */
    var sessionID = "8675309"
    /* D */
    return decrypt(sessionID)
    /* E */
    function decrypt (string) {
        /* F */
        var token = profileID
        /* G */
    }
    /* H */
}
/* I */
logIn()
/* J */
var profileID = 4011989
/* K */
```

1. The variable `username` **has a value** on which lines? (That is: on which lines will `console.log`ing it not return `undefined`?)
    - A, B, I, J, K
    - A and B
    - All lines
    - All lines except A
2. The variable `profileID` **has a value** on which lines?
    - A, B, I, J, K
    - K
    - All lines
    - All lines except A
3. The variable `profileID` **is accessible** on which lines? (That is: on which lines can it be `console.log`ged without throwing an error?)
    - A, B, I, J, K
    - K
    - All lines
    - All lines except A
4. The variable `sessionID` **is accessible** on which lines?
    - C, D, E, F, G, H
    - C, D, E, H
    - All lines
    - All lines except F and G
5. The function `decrypt` **is accessible** on which lines?
    - C, D, E, F, G, H
    - C, D, E, H
    - All lines
    - All lines except F and G

<details>

  <summary><strong>When you've finished...</strong></summary>

  1. All lines except A. The variable is available on all lines due to hoisting, but it only has a value after `username =`
  2. K. The variable is available on all lines due to hoisting, but it only has a value after `profileID =`
  3. All lines.
  4. C, D, E, F, G, H
  5. C, D, E, F, G, H

</details>

## Review Questions (Rest of Class)

1. What is a functions in javascript and how can they be useful?
2. How is a side effect different from an output? 
3. What is the difference between calling and referencing a function?
4. How is a function declaration different than a function expression? 
5. Explain the difference between local and global scope.
6. Explain how hoisting can affect functions.
7. Explain how hoisting can affect variables.  
8. What does DRY mean?

### Bonus: Immediately-Invoked Function Expressions

When you are working on larger, more complex applications (particularly ones with multiple linked scripts), the use of global variables can cause trouble. Since all global variables are defined on the `window` object, declaring too many global variables (commonly called "polluting the global namespace") increases the risk of variables overwriting each other and thereby causing errors.

One simple solution for this is to wrap each script's JavaScript code in an Immediately-Invoked Function Expression (IIFE). An IIFE is a function that, when loaded into the browser, immediately invokes itself and thereby creates a new local scope to enclose all variables within it.

```js
(function () {    // IIFE

  var username = "XxXskaterBoi2004XxX"
  var profileID = 4011989

  function logIn () {
    var sessionID = "8675309"
    var token
    return decrypt(sessionID)

    function decrypt (string) {
      var token = profileID
    }
    return token
  }

  logIn()

})()
```
> NOTE: Using an IIFE would prevent you from being able to access variables and functions within it from the console. Therefore, for now, you should refrain from using it
-------

## References

* [Understanding Scope and Context in JavaScript](http://ryanmorr.com/understanding-scope-and-context-in-javascript/)
* [Everything you wanted to know about JavaScript scope](http://toddmotto.com/everything-you-wanted-to-know-about-javascript-scope/)
