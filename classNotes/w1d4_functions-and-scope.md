![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Functions and Scope
=====

## Opening

Generally speaking, a function is a "subprogram" that can be called by code external (or internal in the case of recursion) to the function.

In JavaScript, **functions are first-class objects**, i.e. they are objects and can be manipulated and passed around just like any other object. Specifically, they are [`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function) objects.

Functions are one of the fundamental building blocks in JavaScript.

<br>

## We Do: Defining Functions

### Function declarations

A **function definition** (also called a **function declaration**, or **function statement**) consists of the function keyword, followed by:

- The **name** of the function.
- A **list of arguments** to the function, enclosed in parentheses and separated by commas.
- The JavaScript **statements** that define the function, enclosed in curly brackets, { }.

For example, the following code defines a simple function named square:

```
function square(number) {
  return number * number;
}
```

### CFU

- What is the argument? `number`
- What is the function statement? `return number * number;`

### Function Expressions

Functions can also be created by a **function expression**. Such a function can be anonymous; it does not have to have a name. For example, the function square could have been defined as:

```
var square = function(number) { return number * number };
```
However, a name can be provided with a function expression and can be used inside the function to refer to itself, or in a debugger to identify the function in stack traces. Don't worry about this at the moment.

#### Passing a function as an argument

Function expressions are convenient when passing a function as an argument to another function.

```
function speak(value){
  return 'hello '+ value;
}

function shout(a, foo) {
  alert(foo(a));
}

shout('world!', speak); 
=> 'hello world!'
```

<br>

## We Do: Calling Functions

Defining a function does not execute it. 

Defining the function simply names the function and specifies what to do when the function is called. 

You call a function by using parenthesis, `()`

```
var hello = function(){console.log("hello")}

hello()
```

Functions must be in scope when they are called, but the function declaration can be **hoisted** (appear below the call in the code), as in this example:

```
console.log(square(5));
function square(n) { return n*n }
=> 25
```

The **scope of a function is the function in which it is declared**, or the entire program if it is declared at the top level.

**Note**: This works only when defining the function using the above syntax (i.e. function funcName(){}). The code below will not work.

```
console.log(square(5));
square = function (n) {
  return n * n;
}
=> Uncaught ReferenceError: square is not defined.
```

There are other ways to call functions.

<br>

## I Do: What is scope?

The JavaScript language has a few concepts of "scope". When talking about scope, you will hear terminology like: 

- `scope`
- `closure`
- `this`
- `namespace`
- `function scope`
- `global scope`
- `lexical scope`
- `public/private scope`

In JavaScript, scope refers to the current context of your code. Scopes can be _globally_ or _locally_ defined. 

### Global Scope

Before you write a line of JavaScript, you're in what we call the `Global Scope`. If we declare a variable, it's defined globally:

```
var name = 'Todd';
```

Global scope is your best friend and your worst nightmare, learning to control your scopes is easy and in doing so, you''ll run into no issues with global scope problems (usually namespace clashes). You'll often hear people saying "Global Scope is _bad_", but never really justifying as to _why_. Global scope isn't bad, you need it to create Modules/APIs that are accessible across scopes, you must use it to your advantage and not cause issues.

### Local scope

A local scope refers to any scope defined past the global scope. There is typically one global scope, and **each function defined has its own (nested) local scope**. Any function defined within another function has a local scope which is linked to the outer function.

### Function scope

#### Can't get inside from outside!

Variables defined inside a function cannot be accessed from anywhere outside the function, because the variable is defined only in the scope of the function.

#### Accessing variables in the same scope

However, a function can access all variables and functions defined inside the scope in which it is defined. 

In other words, a function defined in the global scope can access all variables defined in the global scope. 

```
// The following variables are defined in the global scope
var num1 = 20;
var num2 = 3;

// This function is defined in the global scope
function multiply() {
  return num1 * num2;
}

multiply(); 
=> 60
```

### Nested function scope

A function defined inside another function can also access all variables defined in its parent function and any other variable to which the parent function has access. 

```
var name = "Alex";

function getScore () {
  var num1 = 2,
      num2 = 3;
  
  function add() {
    return name + " scored " + (num1 + num2);
  }
  
  return add();
}

getScore(); 
=> "Alex scored 5"
```

<br>

## We Do: this

A function's `this` keyword behaves a little differently in JavaScript compared to other languages. It also has some differences between strict mode and non-strict mode.

### Global context

In the global execution context (outside of any function), this refers to the global object:

```
this === window
=> true

this.document === document
=> true

this.a = 37;
=> 37
console.log(window.a);
=> 37
```

### Function context 

Inside a function, the value of `this` depends on how the function is called.

```
function f1(){
  return this;
}

f1() === window;
=> true
```

In this case, the value of this is not set by the call. Since the code is not in strict mode, the value of this **must always be an object** so it defaults to the global object.

```
function f2(){
  "use strict"; // see strict mode
  return this;
}

f2() === undefined;
=> true
```

### As an object method

When a function is called as a method of an object, its `this` is set to the object the method is called on.

```
var alex = {name: "Alex",}
alex.speak = function() {
  return this.name;
}

alex.speak();
=> "Alex"
```

<br>

## Closure

Summary of the lesson.

### Questions

Any questions?

<br>
