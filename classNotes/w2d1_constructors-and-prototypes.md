![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Constructors and Prototypes
=====

## Opening

### Object Orientated Programming in Javascript

Following our exploration of creating Javascript objects, it's natural that we now turn our attention to "object oriented (OO) programming" with "classes" in Javascript.

### Review of Class Theory

> "Class/Inheritance" describes a certain form of code organization and architecture -- a way of modeling real world problem domains in our software.

We use classes to help us "model" the world around us. 

### No classes in Javascript?!

Technically, the statement **"JavaScript has no classes"** is correct (prior to ECMAScript6).

**Why?**

Although JavaScript is object-oriented language, it isn't a [class-based](https://en.wikipedia.org/wiki/Class-based_programming) language—it's a [prototype-based](https://en.wikipedia.org/wiki/Prototype-based_programming) language. There are differences between these two approaches, but since it is possible to use JavaScript like a class-based language, many people often simply refer to the **constructor functions as "classes"**.

**Note**: We say that Javascript has prototypical inheritance, not classical inheritance.

<br>

## I Do: Syntax to create an Object

The syntax for creating Objects in Javascript largely come in two forms: 

- the **declarative (literal)** form
- and the **constructed** form

The literal syntax for an object looks like this:

```
var myObj = {
  key: value
};
```

The constructed form looks like this:

```
var myObj = new Object();
myObj.key = value;
```

<br>

## I Do: What is a constructor function?

A constructor is **any Javascript function** which is used as a constructor (to return a new object). The language doesn’t make a distinction. A function can be written to be used as a constructor or to be called as a normal function, or to be used either way.

To *simulate* a class in object-oriented programming, you would write:

```
function Person(name){
  this.name = name;
}
```

### The `new` operator

The [`new`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new) operator in Javascript creates a new instance of a user-defined object type or of one of the built-in object types that has a constructor function.

Now that we have a constructor function, we can use the `new` operator to create a `Person`:

```
var bob = new Person('Bob');
// undefined
```

Just to be sure that `bob` is indeed a `Person`, we can ask:

```
bob instanceof Person;
// true
```

### Assign with `var`

You *could* also call `Person` as a normal function - without the new:

```
Person('Bob')
// undefined
```

However, the `this` value inside the constructor would point to the `window` object and therefore would create a global variable called `name`:

```
window.name
// "Bob"
```

You can prevent this polluting of the namespace by using this trick:

```
function Person(name){
  if (!(this instanceof Person)) {  
    return new Person(name);
  }
  this.name = name;
}

Person("Alex")
// Person {name: "Alex"}
```

**Note**: However, it is much easier to remember to always assign an object to a variable with `var`!

<br>

## I Do: Literal vs Constructor Notation

If you can create objects both with a literal syntax and a constructor syntax, when do you use which one?

**Essentially, they are the same.** 

However, there is a difference if you need **multiple instances** of your object or not. An object defined with a constructor lets you have multiple instances of that object.  Object literals are basically singletons with variables/methods that are all public.

If we created a person with the literal notation:

```
var Person = {
  name: "alex",
}

Person
// Object {name: "alex"}
```

To create another Person, we would need to type this code out again. Or we could use a constructor and do:

```
function Person(name){
  this.name = name;
}

var person1 = new Person("Dave");
var person2 = new Person("John");
```

Our constructor becomes a **template** for creating a new person. However, it's a little bit more than just a template because of the nature of Prototypical inheritance. Instances of an Object have a link to the object that created them.

#### .constructor

To find out which function instantiated a new object, we can use the property [`.constructor`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor).

```
Person.constructor
// Object()
```

A new function is an example of Object() as functions are objects in Javascript!

If we create a person with the declarative syntax, we see that the constructor is now a reference to the custom constructor function.

```
function Person(name){
  this.name = name;
}

var alex = new Person("alex");
alex.constructor
// Person(name)
```

We can also use [`Object.getPrototypeOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf):

```
Object.getPrototypeOf(alex)
// Person {}
```

<br>

## I Do: Prototype chains

### Inheritance

When it comes to inheritance, JavaScript only has one construct: **objects**. 

Each object has an internal **link to another object called its prototype**. That prototype object has an inherited prototype of its own, and so on until an object is reached with null as its prototype. null, by definition, has no prototype, and acts as the final link in this prototype chain.

![spyqq7jwqubh4oyfvqnnw7g](https://cloud.githubusercontent.com/assets/40461/8396752/737ff1c0-1dab-11e5-83b0-4f380980b2b5.png)

Objects are basically key/value pairs. When you ask for a value using a key (property) from an object, Javascript will attempt to find a property in that object instance first, if it cannot find it then Javascript will look for the "default" value in that object’s prototype and so on.

**Note**: This works just like single parent inheritance in a class based language.

Prototype inheritance chains can go as long as you want. But in general it is not a good idea to make long chains as your code can get difficult to understand and maintain.

### Prototype as a pointer

The easiest way to see prototypes in Javascript are as a **pointer to another object saved on the current object**.

![prototype-diagram](https://cloud.githubusercontent.com/assets/40461/8397563/f78b92c8-1dc7-11e5-97fc-79a56d682626.png)

<br>

## We Do: Adding Properties and Methods to Objects

Say we have two people, created by the same constructor function:

```
function Person(name){
  if (!(this instanceof Person)) {  
    return new Person(name);
  }
  this.name = name;
}

var mum = Person("mum");
var dad = Person("dad");
```

### Adding a Property to an Object

Sometimes we want to add new properties to an existing object. This is easy:

```
mum.nationality = "British";
// "British"
```

This property will **only** be added to the instance of the object saved in the variable mum. Dad will be unaffected:

```
dad.nationality
// undefined
```

### Adding a Method to an Object

Adding a method to an existing object is also easy:

```
mum.speak = function() { alert("hello"); }
mum.speak()
```

Again, `dad` will not have this function, only `mum` will have it.


### Adding a property to all instances of an Object

However, what if we wanted to add a new property to both `mum` and `dad` **after** they have been instantiated?

As both objects have the same prototype, we can define a property on that **shared prototype**. This will mean that they will both inherit that property.

```
Person.prototype.species = "Human";
// "Human"

mum.species
// Human

dad.species
// Human
```

Amazing!

<br>

## We Do: Prototypes & Memory

If we define our constructor function like this:

```
function Person(name){
  if (!(this instanceof Person)) {  
    return new Person(name);
  }
  this.name = name;
  this.speak = function(){
    alert("My name is, " + name);
  }
}
```

And we create two new instances:

```
var mum = new Person("mum");
var dad = new Person("dad");


mum.speak == dad.speak;
// false
```

Any method attached via this will get re-declared for every new instance we create, which could affect the memory usage of the application negatively if we wish to create so many instances.

### Use the Prototype

Using Prototype will enable us to easily define methods to all instances of the instances while saving memory. What's great is that the method will **only** be applied to the prototype of the object, so it is only stored in the memory once, because objects coming from the same constructor point to one common prototype object. 

In addition to that, all instances of Person will have access to that method.

```
function Person(name){
  if (!(this instanceof Person)) {  
    return new Person(name);
  }
  this.name = name;
}

Person.prototype.speak = function(){
  alert("My name is, " + name);
}

var mum = Person("mum");
var dad = Person("dad");

mum.speak == dad.speak;
// true
```

So if you have methods that are going to be shared by all instances of an Object, it is 

<br>

## We Do: Multiple inheritance

At the moment, we are only using constructors to create an instance of one Object. You can do multiple inheritance in Javascript using a number of different methods:

### Creating a prototype chain

Setting a constructors `.prototype` property to an instance of another constructor function initializes the prototype chain (sets up inheritance), this is done only once since the prototype object is shared by all initialized objects.

```
function Human(){
  this.alive = true;
}

function Person(name){
  this.name = name;
}

// Would normally be a reference to Person {}
// But we are changing it to Human {} to exend the Human {}
Person.prototype = new Human();

var alex = new Person("Alex");
```
![multiple](https://cloud.githubusercontent.com/assets/40461/8397597/a3e08500-1dc9-11e5-9ba2-a911187730bd.jpg)

Instead of doing: 

```
Person.prototype = new Human();
```

You can actually use the new [`Object.create`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/create) method:

```
Person.prototype = Object.create(Human.prototype);
```

Object.create will not actually run the constructor code, making performance a little better.


### Setting `this` in the parent constructor (Constructor stealing)

We can also inherit the properties of a parent constructor function by using the methods [`.call`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) and [`.apply`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) to explicitly set `this`.

Essentially, we can set `this` in the parent constructor to the the value of the object that is being instantiated. Thus "inheriting" the properties. 

```
function Human(alive){
  this.alive = alive;
}

function Person(name, alive){
  Human.call(this, alive);
  this.name = name;
}

Person.prototype = new Human();

var elvis = new Person("Elvis", false);

elvis
Person {alive: false, name: "Elvis"}
```

This is probably a bit too much at the moment, but it's good to be aware of it.

<br>

## We Do: Object.create

In ECMAScript 5, the latest version of JavaScript available in all modern browsers (Chrome, Firefox, Safari, Opera, IE9+), we have new syntax for creating object-to-object inheritance, based on [Douglas Crockford’s original utility method for simple inheritance](http://javascript.crockford.com/prototypal.html):

[`Object.create`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/create) builds an object that inherits directly from the one passed as its first argument.

You can create a sort of constructor method to use with Object.create

```
var person = {
  alive: true
}

function makePerson(name){
  var p = Object.create(person);
  p.name = name;
  return p;
}

makePerson("Alex");
// Object {name: "Alex"}
```

![alex](https://cloud.githubusercontent.com/assets/40461/8397536/ddd90c1c-1dc6-11e5-89f3-546254537061.jpg)

<br>

## Assess

There has been quite a few terms talked about in this lesson, so let's have a quick practise with this exercise:

### Javascript Prototype Army 

You are going to take over the Javascript world with a new army of Soldier objects.

1. Create a new soldier constructor function that allows you to create soldiers
2. A soldier should be able to have a `name` and `number`
3. The default type of a solder should be `footsoldier`
3. The soldier's `number` should sequentially increase 
4. Each soldier in the army should have the same battleCry, an alert of "FREEDOM!" 
5. Your army should have a general who's type is `general`
6. Your general's number should be incremented inline with your footsolders

<br>

## Closure

Summary of the lesson.

### Questions

Any questions?

<br>