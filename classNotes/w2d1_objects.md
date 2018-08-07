var ![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Objects in JavaScript
=====

## Opening

### What is an object?

Objects in JavaScript, just as many other programming languages, can be compared to objects in real life. The concept of objects in JavaScript can be understood with real life, tangible objects.

In JavaScript, an object is a standalone entity, with **properties** and **type**. Compare it with a cup, for example. A cup is an object, with properties. A cup has a color, a design, weight, a material it is made of, etc. The same way, JavaScript objects can have properties, which define their characteristics.

In JavaScript, **almost everything is an object**. All primitive types except `null` and `undefined` are treated as objects. 

### Collections of name-value pairs

JavaScript objects can be thought of as simple **collections of name-value pairs**. As such, they are similar to:

- Dictionaries in Python
- Hashes in Perl and Ruby
- Hash tables in C and C++
- HashMaps in Java
- Associative arrays in PHP

The fact that this data structure is so widely used is a testament to its versatility. 

The "name" part is a **JavaScript identifier** (either a name, a number, or a string literal), while the value can be **any JavaScript value** — including more objects. This allows you to build data structures of arbitrary complexity.

<br>

## We Do: Creating Objects

There are 4 basic ways to create a new object in Javascript.

#### Object constructor

The [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) constructor creates an object wrapper for the given value.

```
var obj = new Object();
```

#### Object literal syntax

This is also called an [object initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer).

This syntax is also the core of JSON format and should be preferred at all times.

```
var obj = {};
```

#### Constructor function

Alternatively, you can create an object with a constructor function in these two steps:

1. Define the object type by writing a constructor function. There is a strong convention, with good reason, to use a capital initial letter.
2. Create an instance of the object with new.

```
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// Define an object
var You = new Person("You", 24);
```

#### Object Create

Objects can also be created using the [`Object.create()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create) method. This method can be very useful, because it allows you to choose the prototype object for the object you want to create, without having to define a constructor function.

```
var Person = {
  type: "Human",
  displayType: function(){
    console.log(this.type);
  }
}

var person1 = Object.create(Person);
person1.displayType();
=> Human

var person2 = Object.create(Person);
person2.type = "Man";
person2.displayType();
=> Man
```

<br>

## I Do: Object Properties

A JavaScript object has properties associated with it. 

> A property of an object can be explained as a variable that is attached to the object. 

Object properties are basically the same as ordinary JavaScript variables, except for the attachment to objects. The properties of an object define the characteristics of the object. You access the properties of an object with a simple dot-notation:

```
objectName.propertyName
```

You can define a property by assigning it a value using `=` as you would a normal variable.

<br>

## We Do: Create an Object with properties

Let's create an object named myCar and give it properties named make, model, and year as follows:

```
var myCar = new Object();
=> undefined

myCar.make = "Ford";
=> "Ford"

myCar.model = "Mustang";
=> "Mustang"

myCar.year = 1969;
=> 1969

myCar 
=> Object {make: "Ford", model: "Mustang", year: 1969}
```

#### Bracket notation

Properties of JavaScript objects can also be accessed or set using a bracket notation (for more details see [property accessors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_Accessors)). 

**Objects are sometimes called associative arrays**, since each property is associated with a string value that can be used to access it. So, for example, you could access the properties of the myCar object as follows:

```
myCar["make"] = "Ford";
myCar["model"] = "Mustang";
myCar["year"] = 1969;
```

You can also access properties by using a string value that is stored in a variable:

```
var property = "make";
myCar[property] = "Ford";
```

#### Deleting properties

You can remove a non-inherited property by using the [`delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete) operator. The following code shows how to remove a property

```
var myCar = {make: "Ford", model: "Mustang", year: 1969};
delete myCar.make;
myCar
=> {model: "Mustang", year: 1969}
```

<br>

## We Do: Enumarating properties of an Object

Starting with ECMAScript 5, there are three native ways to list/traverse object properties:

- [`for...in`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
- [`Object.keys(o)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
- [`Object.getOwnPropertyNames(o)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames)

They do slightly different different tasks.

#### Loop over an objects properties

You can use the bracket notation with `for...in` to iterate over all the enumerable properties of an object.

```
var myCar = {make: "Ford", model: "Mustang", year: 1969};

function showProps(obj, objName) {
  var result = "";
  for (var i in obj) {
    if (obj.hasOwnProperty(i)) {
        result += objName + "." + i + " = " + obj[i] + "\n";
    }
  }
  return result;
}

showProps(myCar, "Car");
=> "Car.make = Ford
Car.model = Mustang
Car.year = 1969
"
```

<br>

## We Do: Object methods

A method is a function associated with an object, or, simply put, a method is a property of an object that is a function. 

Methods are defined the way normal functions are defined, except that they have to be assigned as the property of an object.

```
var myCar = {
  type: "Honda",
  drive: function() {
    console.log("Vroooom.");
  } 
}
```

You can then call the method:

```
myCar.drive()
```

#### Assigning a previously defined function

```
var reverse = function() { console.log("moooorV."); }

myCar.reverse = reverse;  

myCar.reverse()
=> moooorV.
```

<br>

## We Do: this for object references

JavaScript has a special keyword, `this`, that you can use within a method to refer to the current object. 

**Note**: `this` is a little more complicated than that. However, when the `new` word is used `this` is bound to the Object created.

```
function Person(name) {
  this.name = name;
  this.introduce = function() {
    console.log(this.name);
  }
}

var me = new Person("Alex");
me.introduce();
```

<br>

## We Do: Getters and setters

A getter is a method that gets the value of a specific property. A setter is a method that sets the value of a specific property. You can define getters and setters on any predefined core object or user-defined object that supports the addition of new properties. The syntax for defining getters and setters uses the object literal syntax.

```
var o = {
  a: 7,
  get b() { 
    return this.a + 1;
  },
  set c(x) {
    this.a = x / 2
  }
};

console.log(o.a);
=> 7

console.log(o.b);
=> 8

o.c = 50;
console.log(o.a);
=> 25
```

<br>

## We Do: Private Properties

A [private property](https://developer.mozilla.org/en-US/Add-ons/SDK/Guides/Contributor_s_Guide/Private_Properties) is a property that is only accessible to member functions of instances of the same class. Unlike other languages, JavaScript does not have native support for private properties. However, people have come up with several ways to emulate private properties using existing language features.

### Using Prefixes

A common technique to implement private properties is to prefix each private property name with an underscore. Consider the following example:

```
function Car(make, age) {
  this.make= make;
  this._age = age;
}
=> undefined

var myCar = new Car("Honda", 12);
=> undefined

myCar.age;
=> undefined

myCar.make;
=> "Honda";
```

You can also implement private properties with Closures and WeakMaps (in ECMAScript 6).


<br>

## We Do: Comparing Objects

In JavaScript objects are a reference type. Two distinct objects are never equal, even if they have the same properties. Only comparing the same object reference with itself yields true.

```
var fruit = {name: "apple"};
=> undefined

var fruit2 = {name: "apple"};
=> undefined

fruit == fruit2
=> false

fruit === fruit2
=> false
```

<br>

## Assess: Monkey Exercise

Create a monkey object, which has the following properties:

- name
- species
- foodsEaten

And the following methods:

- eatSomething(thingAsString)
- introduce: introduces self, with name, species, and what it's eaten.

Create 3 monkeys total. Make sure all 3 monkeys have all properties set and
methods defined.

Exercise your monkeys by retrieving their properties and using their methods.
Practice using both syntaxes for retrieving properties.

<br>

## Closure

Summary of the lesson.

### Questions

Any questions?

<br>