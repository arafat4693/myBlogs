# All 4 JavaScript Scopes that you must know

JavaScript has four different scopes: **global**, **module**, **block**, and **function**. Understanding these scopes is essential for any JavaScript developer, as it affects how variables are **accessed** and **declared** within your code. In this blog post, we will go over each of these scopes in detail and provide examples to help you better understand how they work.


## What is scope?
In JavaScript, scope refers to the visibility and accessibility of variables. The best way to think of scope is as a way to help you separate different parts of your code from one another.

Here is an example of **scope** works in javascript:
```js
const globalVar = "global"

function myFunction() {
  const localVar = "local"
  console.log(outerVar, innerVar)
  // Prints: "global", "local"
}

myFunction()
console.log(globalVar, localVar)
//console.log will throw a ReferenceError as localVar is not defined
```
In the example above, the globalVar variable has **global** scope, so it is accessible from both inside and outside the myFunction function. On the other hand, the localVar variable has **local** scope and is only accessible inside the myFunction function. If you try to access it outside the function, you will get a **ReferenceError** because localVar is not defined in the **global** scope.

It's important to understand the concept of scope in JavaScript because it affects how you can use and modify variables in your code.

## Four Scopes
javascript has mainly four scopes in total, they are:

   1. [Global scope](#global-scope)
   2. [Module scope](#module-scope)
   3. [Block scope](#block-scope)
   4. [Function scope](#function-scope)

This seems like a lot to keep track of, but in reality, you will probably use module and block scope for 99% of all the code you write, so it is easier to keep track of. However, you should still pay attention to the other scopes, as it is essential to understand how they work.

## Global scope
The global scope is the outermost scope in JavaScript. All variables and functions that are not inside any other function or block are in the global scope. When you declare a variable or function in the global scope, it is available to be accessed from anywhere in your code.
```js
let globalVar = 'I am a global variable';

function globalFunc() {
  console.log('I am a global function');
}

globalFunc(); // logs 'I am a global function'
console.log(globalVar); // logs 'I am a global variable'

```
One thing to keep in mind is that variables and functions declared in the global scope are also attached to the global object (**window** in the browser). This means that you can also access them as properties of the global object.
```js
console.log(window.globalVar); // logs 'I am a global variable'
window.globalFunc(); // logs 'I am a global function'
```
It is generally considered best practice to avoid using the global scope as much as possible, as it can lead to naming conflicts and can make it harder to understand the code.

## Module scope
Module scope is very similar to **global** scope, but with one minor difference. This means that variables, functions, and other declarations defined in the one file are not accessible outside of the file unless they are explicitly exported. Which is ideal when trying to mentally keep track of everything. To enter **module**
scope, you need to <mark>type="module"</mark> on your script tags.

Here is an example:
```js
<script src="app-1.js" type="module"></script>
<script src="app-2.js" type="module"></script>
```

```js
// app-1.js
const pi = 3.14
console.log(pi)
// Prints: 3.14
```

```js
// app-2.js
console.log(pi)
// Throws ReferenceError as pi is not defined
```
Modules are a powerful way to **organize** and share code in JavaScript, and they are a key feature of the modern JavaScript ecosystem. They allow you to create **reusable**, **self-contained** pieces of code that can be imported and used in multiple places, making it easier to write and maintain large and complex applications.

## Block scope
In JavaScript, block scope refers to the visibility and accessibility of variables within a block of code. A block of code is defined as a set of statements surrounded by curly braces, such as those found in an **if statement**, **for loop**, or **function**.

Variables declared with the **let** and **const** keywords are **block-scoped**, meaning that they are only accessible and can only be modified within the block in which they are declared. This can make it easier to manage and track the variables in your code, as you can be sure that a block-scoped variable will not be modified or accessed outside of its block.

For example:

```js
if (true) {
  let x = 10;
}
console.log(x); // Uncaught ReferenceError: x is not defined
```
In this example, the **let** keyword is used to declare a variable x within the block of the if statement. Because x is block-scoped, it is not accessible outside of the block. Trying to access x outside of the block results in a ReferenceError.

On the other hand, if x were declared with the var keyword, it would be function-scoped and would be accessible outside of the block. In this case, the value 10 would be logged to the console.

It is important to note that block-scoped variables are not accessible outside of the block in which they are declared, even if that block is inside a function or another block. This can be contrasted with function-scoped variables (var keyword), which are accessible throughout the entire function in which they are declared, regardless of any blocks within that function.

For example:

```js
function foo() {
  if (true) {
    let x = 10;
  }
  console.log(x); // Uncaught ReferenceError: x is not defined
}

foo();
```
In this example, the **let** keyword is used to declare a variable x within the block of the if statement. Because x is **block-scoped**, it is not accessible outside of the block, even though it is inside a function. Trying to access x outside of the block results in a **ReferenceError**.

Using block-scoped variables can help prevent unintended modifications and make your code easier to understand and maintain. It is generally recommended to use let or const instead of var when declaring variables in JavaScript.

## Function scope
Variables declared with the **var** keyword are **function-scoped**, meaning that they are accessible and can be modified throughout the entire function in which they are declared. This can lead to potential problems, as it can be difficult to keep track of where a variable is being modified and what its current value is.

For example:

```js
function foo() {
  var x = 10;
}
console.log(x); // Uncaught ReferenceError: x is not defined
```
In this example, the **var** keyword is used to declare a variable x within the function foo. Because x is **function-scoped**, it is not accessible outside of the function. Trying to access x outside of the function results in a ReferenceError.

On the other hand, if x were declared within a block within the function, such as an if statement or for loop, it would be block-scoped and would not be accessible outside of that block.

It is important to note that function-scoped variables are accessible throughout the entire function in which they are declared, regardless of any blocks within that function. This can be contrasted with **block-scoped** variables, which are only accessible and can only be modified within the block in which they are declared.

For example:

```js
function foo() {
  if (true) {
    var x = 10;
  }
  console.log(x); // 10
}

foo();
```
In this example, the **var** keyword is used to declare a variable x within the block of the if statement. Because x is function-scoped, it is accessible throughout the entire function, even though it is declared within a **block**. As a result, the value 10 is logged to the console.

As I said earlier, It is generally recommended to use the **let** or **const** keywords instead of var when declaring variables in JavaScript, as block-scoped variables can help prevent unintended modifications and make your code easier to understand and maintain. However, it is important to understand the difference between function and block scope in order to effectively use variables in your code.

## Multiple Variables With The Same Name
If you have multiple variables with the same name in different scopes, the one that is in the innermost scope takes precedence.

For example:

```js
let name = 'John';  // global scope

function greet() {
  let name = 'Jane';  // local scope
  console.log(`Hello, ${name}!`);  // Output: "Hello, Jane!"
}

greet();
console.log(name);  // Output: "John"
```
In the example above, the **name** variable in the global scope is declared with the value '**John**'. Inside the greet function, a new name variable is declared with the value '**Jane**'. This local variable takes precedence over the global variable when it is accessed within the function, so '**Jane**' is printed to the console. However, when the global name variable is accessed outside of the function, it retains its original value of '**John**'.

You can also use the var keyword to declare variables, but it behaves differently than **let** and **const** in terms of scope. Variables declared with var have function scope, which means they are accessible within the function in which they are declared, as well as any inner functions. If a var variable is declared **outside** of a function, it becomes a global variable.

---

## Conclusion
While it may sound confusing to have four different scopes in JavaScript, it is a bit simpler since we really only care about two of the four scopes. Understanding how these scopes work is also crucial in writing good clean code and might help in the interview.