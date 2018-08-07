![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Closures
=====

## Opening

> A closure is the act of binding all free variables, and functions into a closed expression, that persist beyond the lexical scope from which they were created.

![function](https://cloud.githubusercontent.com/assets/40461/8271947/1fc976be-1829-11e5-99c1-dd941e2507d6.jpg)

Closures are functions that refer to independent (free) variables. In other words, the function defined in **the closure 'remembers' the environment in which it was created**.

Still confused?!

<br>

## I Do: Lexical scoping 

Let's have a look at the following code:

```
function init() {
  var name = "Mozilla";
  function displayName() {
    alert(name);
  }
  displayName();    
}
init();
```

- `init()` creates a local variable name and then a function called `displayName()`
- `displayName()` is an **inner function** that is defined inside `init()` and is only available within the body of that function. 
- `displayName()` has no local variables of its own, however it has access to the variables of outer functions and so can use the variable `name` declared in the parent function.

This is an example of **lexical scoping** (also called Static Scope) in JavaScript, the scope of a variable is defined by its location within the source code. Nested functions have access to variables declared in their outer scope.

<br>

## I Do: Javascript Virtual Machine 

I'm going to talk in VERY general kind of way about how programs are converted from a bunch of text in a file to something that can be run on a computer. *This is a very broad and deep concern in Computer Science.* 

### Javascript Phases

The Javascript Virtual Machine (VM) performs many operations to go from text in a file, i.e. code, to 1's and 0's that are stored in Memory and executed by a CPU.

The phases are:  

- **Load**: Load the javascript file.
- **Compilation**: Compile javascript code in a file to a form that can be executed.
- **Execution**: Run the javascript program.

Part of the Compilation phase, Lexical Analysis, is to look for variable declarations in the source code and build **Variable Scopes**. Scope is also called **Execution Context**. Because it provides a Context for the next phase, Execution.

### Buildng Scope.

Scope is built during the **Lexical Analysis** part of the Compilation phase. When this is done it's called **lexical scope**. This is very common in many programming languages.

<br>

## I Do: Closure

Now consider the following example:

```
function makeFunc() {
  var name = "Mozilla";
  function displayName() {
    alert(name);
  }
  return displayName;
}

makeFunc();
=> function displayName();

var myFunc = makeFunc();
myFunc();
````

If you run this code it will have exactly the same effect as the previous `init()`.

What's different is that the displayName() inner function was returned from the outer function before being executed.

This does feel a little unintuitive. Normally, the local variables within a function only exist for the duration of that function's execution. Once `makeFunc()` has finished executing, it is reasonable to expect that the name variable will no longer be accessible. Since the code still works as expected, this is obviously not the case.

The solution to this puzzle is that **myFunc has become a closure**.

> A closure is a special kind of object that combines two things: a function, and the environment in which that function was created.

The environment consists of any local variables that were in-scope at the time that the closure was created. In this case, `myFunc` is a closure that incorporates both the `displayName` function AND the "Mozilla" string that existed when the closure was created.

#### Another example

Here's a slightly more interesting example — a `makeAdder` function:

```
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
console.log(add5(2));  
=> 7
```

- When you create the closure, `add5` with `makeAdder(5)`, it returns a function that expects to recieve one argument `y`.

In essence, `makeAdder` is a function factory — it creates functions which can add a specific value to their argument. 

**`add5` is a closure**.

```
var add10 = makeAdder(10);
console.log(add10(2));
=> 12
```

**`add10` is another closure**.

`add5` and `add10` are both closures. They share the same function body definition, but store different environments. In `add5`'s environment, `x` is 5. As far as `add10` is concerned, `x` is 10.

<br>

## We Do: Practical Closures

Why are closures actually useful?!

A closure lets you associate some data (the environment) with a function that operates on that data. This has obvious parallels to object oriented programming, where objects allow us to associate some data (the object's properties) with one or more methods.

Much of the code we write in web JavaScript is **event-based** — we define some behavior, then attach it to an event that is triggered by the user (such as a click or a keypress). Our code is generally attached as a callback: a single function which is executed in response to the event.

#### An example

Let's use closures to create some buttons that adjust the size of the text on an HTML page.

#### HTML

First, let's create a file:

```
$ touch closure.html
$ subl .
```

Let's add some basic HTML Boilerplate:

```
<!DOCTYPE>
<html>
<head>
  <title>Practical Closures</title>
</head>
<body>

</body>
</html>
```

Let's add the links to change the font-size:

```
<a href="#" id="size-12">12</a>
<a href="#" id="size-14">14</a>
<a href="#" id="size-16">16</a>
```

#### CSS

And add some basic CSS:

```
 <style>
   body {
     font-family: Helvetica, Arial, sans-serif;
     font-size: 12px;
   }

   h1 {
     font-size: 1.5em;
   }

   h2 {
     font-size: 1.2em;
   }
 </style>
```

#### JS

Let's add Javascript:

```
touch app.js
```

Let's include this file inside the html:

```
<body>
  <script type="text/javascript" src="./app.js"></script>
</body>
```

Inside the js file

```
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);

document.getElementById('size-12').onclick = size12;
document.getElementById('size-14').onclick = size14;
document.getElementById('size-16').onclick = size16;
```

<br>

## I Do: Emulating private methods with closures

JavaScript does not provide a native way to declare private methods. However, it is possible to emulate private methods using closures. 

Here's how to define some public functions that can access private functions and variables, using closures which is also known as the `module pattern`:

```
var counter = (function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  };   
})();

console.log(counter.value()); // logs 0
counter.increment();
counter.increment();
console.log(counter.value()); // logs 2
counter.decrement();
console.log(counter.value()); // logs 1
```

There is a lot going on here but it's useful to look at some closures in the wild!

<br>

## We Do: Self-Executing Anonymous Functions

A related topic, let's have a look at self-executing anonymous functions.

Self-executing functions, actually don't execute themselves... they are invoked like any other function using parenthesis, `()`.

**Note**: Self-executing anonymous functions are examples of, but not the same as [Immediately-Invoked Function Expressions](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression) or **IIFE** for short. 

Why?

- IIFEs don't have to be anonymous, it's only important that they're function expressions.

Example of an IIFE that is not a self-executing anonymous function:

```
(function bleh() {
  alert('I am not anonymous');
})();
```

The function expression is called as soon as it is evaluated. Let's create another self-executing anonymous function:

```
(function(){
  var a = "hello word";
  console.log(a);
})();

console.log(a);
=> Uncaught ReferenceError: a is not defined
```

You can also do (recommended by Douglas Crockford):

```
(function(){
  var a = "hello word";
  console.log(a);
}());

console.log(a);
```

Those two little brackets cause everything contained in the preceding parentheses to be executed immediately. What’s useful here is that JavaScript has function level scoping. All variables and functions defined within the anonymous function aren’t available to the code outside of it, effectively using closure to seal itself from the outside world.

We can pass variables into this self-executing function like this:

```
(function(a){
  var b = a.toUpperCase();
  console.log(b);
})("Hello world!");
```

#### Closure & Self-executing anonymous function

We can use self-executing functions to keep our code tidy! We can also pair them up with closures:

```
var foo = (function(){
  var priv = function() { alert('Hi!'); };
  var publ = function() { priv(); };
  
  return publ;
})();

console.log(foo);
foo();
```

<br>

## Closure

#### Performance considerations

It is unwise to unnecessarily create functions within other functions if closures are not needed for a particular task, as it will negatively affect script performance both in terms of processing speed and memory consumption.

### Questions

Any questions?

<br>