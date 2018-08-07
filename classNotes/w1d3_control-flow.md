![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Control Flow
=====

## Opening

JavaScript supports a compact set of statements, specifically control flow statements, that you can use to incorporate a great deal of interactivity in your application.

<br>

## I Do: Block Statements

The most basic control flow statement is a **block statement**, used to group other statements. The block is delimited by a pair of curly brackets:

```
{ 
  console.log("hello"); 
  console.log("roar"); 
}
```

#### Block scope

Block statements do not introduce a scope.

```
var x = 1;
{
  var x = 2;
}
console.log(x); // outputs 2
```

Only functions introduce scope in Javascript. 

<br>

## I Do: Conditional statements

Conditional statements are a way of essentially skipping over a block of code if it does not pass a boolean expression. JavaScript supports two conditional statements: `if`...`else` and `switch`.

#### if...else statement

- `if(expr) { code }`: run the `code` block if `expr` is `true`

```
if (1 > 0) { console.log("hi") }
=> hi
```

You may also compound the statements using `else if` to have multiple conditions tested in sequence, as follows:

```
var name = "kittens";
if (name == "puppies") {
  name += "!";
} else if (name == "kittens") {
  name += "!!";
} else {
  name = "!" + name;
}
=> "kittens!!"
```

**Note**: It is advisable to not use simple assignments in a conditional expression, because the assignment can be confused with equality when glancing over the code. For example, do not use the following code:

```
if (x = 3) {
console.log("boo");
}
```

#### Ternary Operator

JavaScript has a ternary operator for conditional expressions:

```
var age = 12;
=> undefined

var allowed = (age > 18) ? "yes" : "no";
=> undefined

allowed
=> "no"
```

<br>

## We Do: Truthy & Falsy

#### All of the following become false when converted to a Boolean

- `false`
- `0`
- `""` (empty string)
- `NaN`
- `null`
- `undefined`

#### All other values become true when converted to a Boolean

Do not confuse the primitive boolean values `true` and `false` with the true and false values of the Boolean object. For example:

```
var b = new Boolean(false);
if (b) { console.log("true") }
=> true
```

We can somethings truthyness using the `!` operator

```
!!1
=> true
	
!!0
=> false
	
!!-1
=> true
	
!![]
=> true
	
!!{}
=> true
	
!!null
=> false
	
!!""
=> false
```

<br>

## We Do: Boolean/Logical Operators

[Logical operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators) are typically used with Boolean (logical) values. When they are, they return a Boolean value `true` or `false`.

There are two types of binary operators that work with booleans, (a binary operator just requires two arguments).

* **AND**, denoted `&&` 
* **OR**, denoted `||`

There is a third unary operatory, (a unary operator that requires just one argument).

* **NOT**, denoted `!`

#### && (AND)

The `&&` operator requires both left and right values to be `true` in order to return `true`, i.e.
	
```
true && true
=> true
```

Any other combination is false.

```
true && false
=> false

false && false
=> false
```

#### || (OR)

The `||` operator requires just one of the left or right values to be `true` in order to return true.

```
true || false
=> true

false || true
=> true

false || false
=> false
```

Only `false || false` will return `false`

#### ! (NOT)
	
The `!` takes a value and returns the opposite boolean value, i.e. 

```
!(true)
=> false
```

The `&&` and `||` operators use short-circuit logic, which means whether they will execute their second operand is dependent on the first. This is useful for checking for null objects before accessing their attributes:

```
var name = o && o.getName();
```

Or for setting default values:

```
var name = otherName || "default";
```

<br>

## We Do: Comparison Operators

[Comparisons](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators) in JavaScript can be made using `<`, `>`, `<=` and `>=`. These work for both strings and numbers. 

```
"A" > "a" 
=> false

"b" > "a"
=> true

12 > "12"
false

12 >= "12"
true
```

### Equality Operator

#### ==

Equality is a little less straightforward. The double-equals operator performs **type coercion** if you give it different types, with sometimes interesting results:

```
"dog" == "dog";
=> true

1 == true; 
=> true
```

#### ====

To avoid type coercion, **use the triple-equals operator**. So to compare two values in Javascript for equality testing we use `===`, which will check the sameness of the thing on the left with the thing on the right. 

**Note** sameness is a very fuzzy word and thus `===` is also very fuzzy concept, which should be approached with caution in every language. 

```
1 === true;
=> false

true === true; 
=> true

"hello" === "hello"
=> true
```

However, there are some incidents when it does not:

```
{} === {}
Uncaught SyntaxError: Unexpected token ===

[] === []
=> false
```

**Explanation**

The second set of examples fail because both **object literals** and **arrays** are objects, and not just values like strings, numbers, and booleans. Objects can be complex collections of values in memory that we  are referring to in a program, and so, we only reference each object by an id to simplify things. However, that means when we go to compare the two objects we don't care if they look like similar collections. We only compare their respective ids when checking for equality, and each `{}` or `[]` represents a new object with it's own unique id.

Arrays and objects are called **reference** types for the above reasons, so be careful with using them too intuitively.

#### != and !==

There are also `!=` and `!==` operators.

JavaScript also has [bitwise operations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators). If you want to use them, they're there.

<br>

## We Do: Switch Statement

The switch statement can be used for multiple branches based on a number or string:

```
var food = "apple";

switch(food) {
  case 'pear':
    console.log("I like pears");
    break;
  case 'apple':
    console.log("I like apples");
    break;
  default:
    console.log("No favourite");
}
=> I like apples
```

The default clause is optional. You can have expressions in both the switch part and the cases if you like; comparisons take place between the two using the `===` operator:

<br>

## We Do: While and Do-While

The while statement creates a loop that executes a specified statement as long as the test condition evaluates to true. The condition is evaluated before executing the statement.

JavaScript has `while` loops and `do-while` loops. The first is good for basic looping; the second for loops where you wish to ensure that the body of the loop is executed at least once:

```
while (true) {
  // an infinite loop!
}
```

This should be enough to break a browser.

```
var input = 0;
do {
  console.log(input++);
} while (input < 10);
```

<br>

## We Do: Iteration

Iterating is a way of incrementally repeating a task. 

#### for

You can iterate over an array with:

```
var a = [1,2,3,4,5];
for (var i = 0; i < a.length; i++) {
  console.log(i);
}
```

This is slightly inefficient as you are looking up the length property once every loop. An improvement is to chain the `var` assignment:

```
var a = [1,2,3,4,5];
for (var i = 0, len = a.length; i < len; i++) {
  console.log(i);
}
```

A nicer-looking but limited idiom is:

```
var a = [1,2,3,4,5];
for (var i = 0, item; item = a[i++];) {
*   console.log(iten);
}
```

Here we are setting up two variables. The assignment in the middle part of the `for` loop is also tested for truthfulness — if it succeeds, the loop continues. Since `i` is incremented each time, items from the array will be assigned to item in sequential order. The loop stops when a "falsy" item is found (such as `undefined`).

This trick should only be used for arrays which you know do not contain "falsy" values (arrays of objects or [DOM](https://developer.mozilla.org/en-US/docs/Glossary/DOM) nodes for example). If you are iterating over numeric data that might include a 0 or string data that might include the empty string you should use the `i, len` idiom instead.

#### forEach 

Another way of iterating over an array that was added with ECMAScript 5 is [`forEach()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach):

```
["dog", "cat", "hen"].forEach(function(currentValue, index, array) {
   console.log("I want a ", currentValue);
   console.log(array[index]);
});
```

<br>

## Closure

Summary of the importance of control structures in basic programming

### Questions

Any questions?

<br>