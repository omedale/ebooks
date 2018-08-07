![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Javascript `this`
=====

## Opening

What `this` is refers to in Javascript code, (`this` binding) is a constant source of confusion for the new JavaScript developer.

#### Learn what `this` is not

First have to learn what `this` is *not*, despite any assumptions or misconceptions that may lead you down those paths: 

- `this` is not a reference to the function itself
- `this` is not a reference to the function's *lexical* scope

#### Learn what `this` is

`this` is actually a binding that is made when a function is invoked, and *what* it references is determined **entirely by the call-site where the function is called**.

<br>

## I Do: Common `this` confusions

The name "this" creates confusion when developers try to think about it too literally. There are two common misconceptions about `this`:

### Itself

The first common temptation is to assume `this` refers to the function itself.

Let's have a look at the code in `itself.js`, uncomment:

```
 <script type="text/javascript" src="./js/itself.js"></script>
```

Let's consider this code:

```
function foo(num) {
  console.log("foo: " + num);

  // Does this keep track of how many times `foo` is called?
  this.count++;
}

foo.count = 0;

for (var i=0; i<10; i++) {
  if (i > 5) {
    foo(i);
  }
}

console.log("foo.count: " + foo.count); // 0
console.log("window.count: " + count);  // NaN
```

`foo.count` is still 0, even though the four console.log statements clearly indicate `foo(..)` was in fact called four times.

When the code executes `foo.count = 0`, indeed it's adding a property `count` to the function object `foo`. But for the `this.count` reference inside of the function, `this` is not in fact pointing at all to that function object.

### Its Scope 

The next most common misconception about the meaning of `this` is that it somehow refers to the function's scope. It's a tricky question, because in one sense there is some truth, but in the other sense, it's quite misguided.

Let's have a look at the code in `its-scope.js`, re-comment the itself.js file and uncomment `its-scope.js`:

```
 <!-- <script type="text/javascript" src="./js/itself.js"></script> -->
 <script type="text/javascript" src="./js/its-scope.js"></script>
```

Let's look at this code:

```
function foo() {
  var a = 2;
  this.bar();
}

function bar() {
  console.log(this.a);
}

foo(); //ReferenceError: a is not defined
```

The developer who is attempting to use `this` to create a bridge between the lexical scopes of the function of `foo()` and the function of `bar()`, so that `bar()` has access to the variable `a` in the inner scope of `foo()`. 

**No such bridge is possible!**

<br>

## I Do: Finding the call-site

To understand `this` binding, we have to understand the call-site: 

> Call-site is the location in code where a function is called (**not where it's declared**). 

We must inspect the call-site to answer the question: what's *this* `this` a reference to?

Finding the call-site is generally: "go locate where a function is called from", but it's not always that easy, as certain coding patterns can obscure the *true* call-site.

Take a look at `call-site.js`:

```
function baz() {
  // call-stack is: `baz`
  // so, our call-site is in the global scope

  console.log( "baz" );
  bar(); // <-- call-site for `bar`
}

function bar() {
  // call-stack is: `baz` -> `bar`
  // so, our call-site is in `baz`

  console.log( "bar" );
  foo(); // <-- call-site for `foo`
}

function foo() {
  // call-stack is: `baz` -> `bar` -> `foo`
  // so, our call-site is in `bar`

  console.log( "foo" );
}

baz(); // <-- call-site for `baz`
```

Take care when analyzing code to find the actual call-site (from the call-stack), because it's the **only thing that matters for `this` binding**.

**Note**: You can visualize a call-stack in your mind by looking at the chain of function calls in order, as we did with the comments in the above snippet. But this is painstaking and error-prone. Another way of seeing the call-stack is using a debugger tool in your browser.

<br>

## We Do: Default Binding 

By default, `this` is bound to the global object (`window` in a browser)

In the global scope, when the code is executing in the browser, all global variables and functions are defined on the `window` object. Therefore, when we use `this` in a global function, it refers to (and has the value of) the global window object

```
function foo() {
  console.log(this.a);
}

var a = 2;

foo(); //2
alert(this); //[object Window]
```

#### Strict Mode

Note that when we use strict mode, `this` holds the value of `undefined` in global functions and in anonymous functions that are not bound to any object.

Take a look at `default-binding-strict.js`:

```
function foo() {
  "use strict";

  console.log( this.a );
}

var a = 2;

foo(); // TypeError: `this` is `undefined`
```

<br>

## I Do: Implicit Binding 

Something else to consider: does the call-site have a context object, also referred to as an owning or containing object?

Take a look at `implicit-binding.js`:

```
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
  foo: foo
};

obj.foo(); // 2
```

Because `obj` is the `this` for the `foo()` call, `this.a` is synonymous with `obj.a`.

<br>

## I Do: Explicit Binding 

Invoking `foo` with explicit binding by `foo.call(..)` or `foo.apply(..)` allows us to force its `this` to be `obj`.

```
function foo() {
  console.log( this.a );
}

var obj = {
  a: 2
};

foo.call(obj); // 2
```

For more information see: 

- [`.call()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
- [`.apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)


<br>

## I Do: `new` Binding

By calling `foo(..)` with `new` in front of it (constructor), we've constructed a new object and set that new object as the `this` for the call of `foo(..)`:

```
function foo(a) {
  this.a = a;
}

var bar = new foo(2);
console.log(bar.a); // 2
```

<br>

## We Do: Determining `this`

Now, we can summarize the rules for determining `this` from a function call's call-site, in their order of precedence. Ask these questions in this order, and stop when the first rule applies.

**Question 1.** Is the function called with `new` (**new binding**)? If so, `this` is the newly constructed object.

```
var bar = new foo();
```

**Question 2.**  Is the function called with `call` or `apply` (**explicit binding**), even hidden inside a `bind` *hard binding*? If so, `this` is the explicitly specified object.

```
var bar = foo.call(obj2);
```

**Question 3.** Is the function called with a context (**implicit binding**), otherwise known as an owning or containing object? If so, `this` is *that* context object.

```
var bar = obj1.foo();
```

**Question 4.** Otherwise, default the `this` (**default binding**). If in `strict mode`, pick `undefined`, otherwise pick the `global` object.

```
var bar = foo();
```

That's it. That's *all it takes* to understand the rules of `this` binding for normal function calls. Well... almost.

There are a few exceptions but for the most part, you can't go wrong with this strategy.

<br>

## Closure

In summary, every execution context has an associated `ThisBinding` whose lifespan is equal to that of the execution context and whose **value is constant**. There are three types of execution context: 

- global
- function 
- evaluation

Here is a table summary:

| Execution Context | Syntax of function call | Value of this |
|-------------------|-------------------------|---------------|
| Global | n/a | global object (e.g. `window`)
| Function | Method call: `myObject.foo();` | `myObject`
| Function | Baseless function call: `foo();` | global object (e.g. `window`) (undefined in strict mode)
| Function | Using call: `foo.call(context, myArg);` | context
| Function | Using apply: `foo.apply(context, [myArgs]);` | context
| Function | Constructor with new: `var newFoo = new Foo();` | the new instance (e.g. `newFoo`)
| Evaluation | n/a | value of `this` in parent context

<br>

###Questions

Any questions?

<br>