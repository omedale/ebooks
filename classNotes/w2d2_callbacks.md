![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Callbacks
=====

## Opening

Callback functions are derived from a programming paradigm known as **functional programming**. At a fundamental level, functional programming specifies the use of functions as arguments. Functional programming was—and still is, though to a much lesser extent today—seen as an esoteric technique of specially trained, master programmers.

<br>

## I Do: What is a Callback/Higher-order Function?

A callback function, also known as a higher-order function, is a function that is passed to another function (let’s call this other function “otherFunction”) as a parameter, and the callback function is called (or executed) inside the otherFunction. A callback function is essentially a pattern (an established solution to a common problem), and therefore, the use of a callback function is also known as a callback pattern.

#### An example:

```
var element = document.getElementsByTagName("body")[0];

element.addEventListener("click", function(){
  console.log("Executed in the callback function.");
})
```

Another example within a `forEach` loop:

```
var friends = ["Mike", "Stacy", "Andy", "Rick"];
​
friends.forEach(function (eachName, index){
  console.log(index + 1 + ". " + eachName);
});
```

We have passed an anonymous function (a function without a name) to the forEach method as a parameter.

We could have re-written this using a named function

```
function loopyName(eachName, index){
  console.log(index + 1 + ". " + eachName);
};

var friends = ["Mike", "Stacy", "Andy", "Rick"];
friends.forEach(loopyName);
```

Cool!

<br>

## We Do: How Callback Functions Work?

- We can pass functions around like variables and return them in functions and use them in other functions. 
- When we pass a callback function as an argument to another function, we are only **passing the function definition**. 
- We are **not executing the function** in the parameter. In other words, we aren’t passing the function with the trailing pair of executing parenthesis `()` like we do when we are executing a function.

Note that the callback function is not executed immediately. It is “called back” (hence the name) at some specified point inside the containing function’s body. 

#### Callback Functions Are Closures!

When we pass a callback function as an argument to another function, the callback is executed at some point inside the containing function’s body just as if the callback were defined in the containing function. 

This means the callback is a closure.

Closures have access to the containing function’s scope, so the callback function can access the containing functions’ variables, and even the variables from the global scope.

<br>

## We Do: Named Functions as Callbacks

It is a common pattern to use an anonymous function as a callback. However, you can use a named function!

Consider this code (copy into Sublime if needed):

```
// global variable​
​var allUserData = [];

// generic logStuff function that prints to console​
​function logStuff(userData) {
  if (typeof userData === "string") {
    console.log(userData);
  } else if (typeof userData === "object") {
    for (var item in userData) {
      console.log(item + ": " + userData[item]);
    }
​  }
}

// A function that takes two parameters, the last one a callback function
​function getInput(options, callback) {
  allUserData.push(options);
  callback(options);
}

// When we call the getInput function, we pass logStuff as a parameter.​
​// logStuff will called back (or executed) inside the getInput function​
getInput({name:"Alex", speciality:"JavaScript"}, logStuff);
```

<br>

## We Do: Pass Parameters to Callback Functions

Since the callback function is just a normal function when it is executed, we can pass parameters to it!

We can pass any of the containing function’s properties (or global properties) as parameters to the callback function. 

<br>

## We Do: Ensure Callback is a Function

You can check a callback is a function before executing it:

```
if (typeof callback === "function") {
  ​callback(options);
}
```

<br>

## We Do: `this` and Callbacks Problems

When the callback function is a method that uses the `this` object, we have to modify how we execute the callback function to preserve the `this` object context.

```
// Define an object with some properties and a method​
​// We will later pass the method as a callback function to another function​
​var clientData = {
  id: 094545,
  fullName: "Not Set",
  // setUserName is a method on the clientData object​
  setUserName: function (firstName, lastName)  {
    // this refers to the fullName property in this object​
    this.fullName = firstName + " " + lastName;
  }
}
​
​function getUserInput(firstName, lastName, callback)  {
  callback(firstName, lastName);
}

getUserInput("Barack", "Obama", clientData.setUserName);

console.log (clientData.fullName);
=> Not Set

console.log (window.fullName);
=> Barack Obama
```

Since `getUserInput` is a global function, `this` points to the window object.

#### Use the `Call` or `Apply` Function To Preserve `this`

We can fix the preceding problem by using the `Call` or `Apply` function.

Every function in JavaScript has two methods: `Call` and `Apply`. And these methods are used to set the this object inside the function and to pass arguments to the functions.

- [`Call`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) takes the value to be used as the `this` object inside the function as the **first parameter**, and the remaining arguments to be passed to the function are passed individually (separated by commas of course).
- [`Apply`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) function’s first parameter is also the value to be used as the `this` object inside the function, while the last parameter is an array of values (or the arguments object) to pass to the function.

```
// Define an object with some properties and a method​
​// We will later pass the method as a callback function to another function​
​var clientData = {
  id: 094545,
  fullName: "Not Set",
  // setUserName is a method on the clientData object​
  setUserName: function (firstName, lastName)  {
    // this refers to the fullName property in this object​
    this.fullName = firstName + " " + lastName;
  }
}
​
​function getUserInput(firstName, lastName, callback, callbackObj)  {
  // The use of the Apply function below will set the this object to be callbackObj​
  callback.apply(callbackObj, [firstName, lastName]);
}
 getUserInput("Barack", "Obama", clientData.setUserName, clientData);

console.log (clientData.fullName);
=> Barack Obama
```

<br>

## We Do: Callback hell

What is What is ["callback hell"](http://callbackhell.com/) - aka. pyramid of doom.

![pyr-1](https://cloud.githubusercontent.com/assets/40461/8271348/2f04d48a-180a-11e5-8d5f-31677648b103.png)

Asynchronous javascript, or javascript that uses callbacks, is hard to get right intuitively. A lot of code ends up looking like this:

```
fs.readdir(source, function(err, files) {
  if (err) {
    console.log('Error finding files: ' + err)
  } else {
    files.forEach(function(filename, fileIndex) {
      console.log(filename)
      gm(source + filename).size(function(err, values) {
        if (err) {
          console.log('Error identifying file size: ' + err)
        } else {
          console.log(filename + ' : ' + values)
          aspect = (values.width / values.height)
          widths.forEach(function(width, widthIndex) {
            height = Math.round(width / aspect)
            console.log('resizing ' + filename + 'to ' + height + 'x' + height)
            this.resize(width, height).write(destination + 'w' + width + '_' + filename, function(err) {
              if (err) console.log('Error writing file: ' + err)
            })
          }.bind(this))
        }
      })
    })
  }
})
```

See all the instances of `function` and `})`? Eek! This is affectionately known as callback hell.

Here are two solutions to this problem:

1. **Name your functions** and declare them and pass just the name of the function as the callback, instead of defining an anonymous function in the parameter of the main function.
2. **Modularity**: Separate your code into modules, so you can export a section of code that does a particular job. Then you can import that module into your larger application.

You will get a chance to practise this, the more Javascript code you write.

<br>

## Closure

Summary of the lesson.

### Questions

Any questions?

<br>