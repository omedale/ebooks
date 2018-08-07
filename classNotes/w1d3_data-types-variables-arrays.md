![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Data Types, Variables and Arrays
=====

## Opening

JavaScript is an object oriented dynamic language with types and operators, standard built-in objects, and methods. Its syntax comes from the Java and C languages, so many structures from those languages apply to JavaScript as well. 

#### Chrome Console

For this lesson, we're going to use the Chrome Console shell.

Let's open up the console, `cmd+alt+j`.

<br>

## I Do: Data Types

Let's start off by looking at the building block of any language: the types. JavaScript programs manipulate values, and those values all belong to a type. JavaScript's types are:

### Primative Data Types

- [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
- [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
- [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)

### Composite Data Types

- [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
  - [`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function) 
  - [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
  - [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
  - [`RegExp`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
  
### Special Data Types

* [`null`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)
* [`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)

Coming soon in in ECMAScript 6!

- [`Symbol`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
    
And there are some built-in [`Error`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error) types as well. Things are a lot easier if we stick with the list above, though.

#### typeof()

To check if a variable is a certain type, we can use [`typeof()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)

```
typeof 37 === 'number';
=> true

typeof {} === 'object';
=> true

typeof null === 'object';
=> true

typeof function(){} === 'function';
=> true
```

<br>

## We Do: Numbers

Numbers in JavaScript are **"double-precision 64-bit format IEEE 754 values"**, according to the spec. This has some interesting consequences. There's no such thing as an integer in JavaScript, so you have to be a little careful with your arithmetic if you're used to math in C or Java. Watch out for stuff like:

```
0.1 + 0.2
=> 0.30000000000000004
```

In practice, integer values are treated as 32-bit ints (and are stored that way in some browser implementations), which can be important for bit-wise operations.

#### Arithmetic Operators

The standard [arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators#Arithmetic_operators) are supported, including addition, subtraction, modulus (or remainder) arithmetic and so forth. 

```
1 + 2
=> 3 

2 - 5
=> -3

5 / 2
=> 2.5

6 * 2
=> 12
```

#### Math Object

There's also a built-in object called [`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) if you want to perform more advanced mathematical functions and constants:

```
Math.sqrt(9);
=> 3

Math.round(9.5)
=> 10
```

### Converting Strings to Integers

#### parseInt()

You can convert a string to an integer using the built-in [`parseInt()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt) function. This takes the base for the conversion as an optional second argument, which you should always provide:

```
parseInt("123", 10); 
=> 123

parseInt("010", 10); 
=> 10
```

If you want to convert a binary number to an integer, just change the base:

```
parseInt("11", 2);
=> 3
```

#### parseFloat()

Similarly, you can parse floating point numbers using the built-in [`parseFloat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat) function which uses base 10 always unlike its `parseInt()` cousin.

```
parseFloat("11.2");
=> 11.2
```

#### Unary operator

You can also use the unary `+` operator to convert values to numbers:

```
+"42"; 
=> 42
```

### Assess

Ask the class, what will these return?

```
parseInt("10.2abc", 10)
=> 10

parseFloat("10.2abc")
=> 10.2

+"10.2abc"
=> NaN
```

The `parseInt()` and `parseFloat()` functions parse a string until they reach a character that isn't valid for the specified number format, then return the number parsed up to that point. However the "+" operator simply converts the string to `NaN` if there is any invalid character in it. 

#### NaN

A special value called [`NaN`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN) (short for "Not a Number") is returned if the string is non-numeric:

```
parseInt("hello", 10);
=> NaN
```

**`NaN` is toxic**: if you provide it as an input to any mathematical operation the result will also be `NaN`:

```
NaN + 5;
=> NaN
```

You can test for `NaN` using the built-in [`isNaN()`](ttps://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN) function:

```
isNaN(NaN); 
=> true
```

#### Infinity

JavaScript also has the special values [`Infinity`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Infinity) and `-Infinity`:

```
1 / 0; 
=> Infinity

-1 / 0; 
=> -Infinity
```

You can test for `Infinity`, `-Infinity` and `NaN` values using the built-in [`isFinite()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isFinite) function:

```
isFinite(1/0); 
=> false

isFinite(-Infinity); 
=> false

isFinite(NaN); 
=> false
```

<br>

## We Do: Strings

Strings in JavaScript are sequences of characters. More accurately, they are sequences of [Unicode characters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Values,_variables,_and_literals#Unicode), with each character represented by a 16-bit number. 

#### Length 

To find the length of a string, access its [`length`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length) property:

```
"hello".length;
=> 5
```

#### Wait, Strings have methods?!

There's our first brush with JavaScript objects! Did I mention that you can use strings like objects too? 

Strings have other [methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String#Methods) as well that allow you to manipulate the string and access information about the string:

```
"hello".charAt(0); 
=> "h"

"hello, world".replace("hello", "goodbye"); 
=> "goodbye, world"

"hello".toUpperCase();
=> "HELLO"
```

There is no method for built-in capitalization. You would have to do:

```
var greeting = "hello";
greeting.charAt(0).toUpperCase() + greeting.slice(1);
```

#### String concatination

The [`+` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Addition) also does string concatenation:

```
"hello" + " world";
=> "hello world"
```

If you add a string to a number (or other value) everything is converted in to a string first. This might catch you up:

```
"3" + 4 + 5;
=> "345"

3 + 4 + "5"; 
=> "75"
```

**Note**: Adding an empty string to something is a useful way of converting it.

<br>

## We Do: Null & Undefined

JavaScript distinguishes between: 

- `null` a value that indicates a deliberate non-value
- `undefined` that indicates an uninitialized value — that is, a value hasn't even been assigned yet. 

We'll talk about variables later, but in JavaScript it is possible to declare a variable without assigning a value to it. If you do this, the variable's type is `undefined`. `undefined` is actually a constant.

```
var a;
=> undefined

a
=> undefined
```

<br>

## We Do: Booleans

JavaScript has a boolean type, with possible values `true` and `false` (both of which are keywords). Any value can be converted to a boolean according to the following rules:

#### All of the following become false when converted to a Boolean

- `false`
- `0`
- `""` (empty string)
- `NaN`
- `null`
- `undefined`

#### All other values become true when converted to a Boolean

You can perform this conversion explicitly using the `Boolean()` function:

```
Boolean(""); 
=> false

Boolean(234); 
=> true

Boolean("a");
=> true
```

However, this is rarely necessary, as JavaScript will silently perform this conversion when it expects a boolean, such as in an `if` statement (see below). For this reason, we sometimes speak simply of "true values" and "false values," meaning values that become `true` and `false`, respectively, when converted to booleans. 

Alternatively, such values can be called **"truthy"** and **"falsy"**, respectively.

Boolean operations such as `&&` (logical _and_), `||` (logical _or_), and `!` (logical _not_) are supported.

<br>

## We Do: Variables

JavaScript's numeric operators are `+`, `-`, `*`, `/` and `%`.

#### Assignment Operators

Values are assigned using `=`, and there are also compound assignment statements such as `+=` and `-=`. 

```
var x = 1;
=> 1 

x += 5
=> 6
```

You can use `++` and `--` to increment and decrement respectively. These can be used as prefix or postfix operators.

#### Always use var!

New variables in JavaScript are declared using the [`var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var "/en/JavaScript/Reference/Statements/var") keyword:

```
var a;
=> undefined
```

If you declare a variable without assigning any value to it, its type is `undefined`.

```
var name = "Alex";
=> undefined

name
=> "Alex"
```

#### Global variables

It is not possible to define variables without var.

```
x = 1
=> 1
```

The above is a property assignment. First Javascript tries to resolve `x` against the scope chain. If it finds `x` anywhere in that scope chain, it performs an assignment; if it doesn't find `x`, **only** then does it create `x` property on a global object (**which is a top level object in a scope chain**).

* ```
window.x
=> 1
```

Now, notice that it doesn't declare a global variable, it creates a global property.

#### Block scope

An important difference from other languages like Java is that in JavaScript, **blocks do not have scope**; only functions have scope. (The block is delimited by a pair of curly brackets.)

```
{
  statement_1;
  statement_2;
}
```

So if a variable is defined using `var` in a compound statement (for example inside an `if` control structure), it will be visible to the entire function. 

**Note**: However, starting with ECMAScript Edition 6, [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) and [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) declarations allow you to create block-scoped variables.

<br>

## We Do: Arrays

JavaScript arrays are used to store multiple values in a single variable.

#### Using the JavaScript Keyword new

One way of creating arrays is as follows:

```
var a = new Array();
=> undefined

a[0] = "dog";
=> "dog"

a[1] = "cat";
=> "cat"

a[2] = "hen";
=> "hen"

a
=> ["dog", "cat", "hen"]

a.length;
=> 3
```

#### Using an Array Literal

A more convenient notation is to use an array literal:

```
var a = ["dog", "cat", "hen"];

a.length;
=> 3
```

#### Length method

The `length` method works in an interesting way in Javascript. It is always one more than the highest index in the array.

So `array.length` isn't necessarily the number of items in the array. Consider the following:

```
var a = ["dog", "cat", "hen"];
a[100] = "fox";
a.length; // 101
```

**Remember**: the length of the array is one more than the highest index.

#### Getting from an array

If you query a non-existent array index, you get `undefined`:

```
var a = ["dog", "cat", "hen"];
=> undefined

typeof a[90]; 
=> undefined
```

<br>

## We Do: Array methods

* Arrays come with a number of methods. See also the [full documentation for array methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).

- `a.toString()` 

Returns a string with the `toString()` of each element separated by commas.

- `a.toLocaleString()`

Returns a string with the `toLocaleString()` of each element separated by commas.

- `a.concat(item1[, item2[, ...[, itemN]]])`

Returns a new array with the items added on to it.

- `a.join(sep)`

Converts the array to a string - values delimited by the `sep` param 

- `a.pop()`

Removes and returns the last item.

- `a.push(item1, ..., itemN)`

`Push` adds one or more items to the end.

- `a.reverse()`

Reverse the array.

- `a.shift()`

Removes and returns the first item.

- `a.slice(start, end)`

Returns a sub-array.

- `a.sort([cmpfn])` 

Takes an optional comparison function. 

- `a.splice(start, delcount[, item1[, ...[, itemN]]])` 

Lets you modify an array by deleting a section and replacing it with more items.

- `a.unshift([item])`

Prepends items to the start of the array. 


<br>

## Closure

Summary of the lesson.

### Wat?!

Some strange Javascript...

```
[] + []
=> ""

[] + {}
=> [object Object]

{} + []
=> 0

{} + {}
=> NaN

Array(16)

Array(16).join("wat")

Array(16).join("wat + 1")

Array(16).join("wat" - 1) + " Batman!"
```

From [here](https://www.destroyallsoftware.com/talks/wat).

### Questions

Any questions?

<br>
