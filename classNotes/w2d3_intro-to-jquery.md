![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Intro to jQuery
=====

## Opening: What is jQuery?

> **jQuery:** The Write Less, Do More, JavaScript Library.

Not to be confused with [Jake Weary](https://en.wikipedia.org/wiki/Jake_Weary).

jQuery is a 3rd-party library that makes tasks like HTML document traversal and manipulation, event handling, animation, and Ajax much simpler with an easy-to-use API that works across a multitude of browsers.

### What is a library?

A **library** is just a collection of code, predominantly reusable methods, that serve a particular purpose.

### So, as a library, what does jQuery offer us?

- jQuery helps us manipulate the DOM, allowing us to perform complex manipulations in less code with less hassle
- jQuery's syntax was developed to mimic CSS selector syntax, making code easier to develop, read, and manage
- The syntax is shorter, and we're lazy!
- jQuery deals with many cross-browser compatibility issues for us

### jQuery is just Javascript

> jQuery is just Javascript

> jQuery is just Javascript

> jQuery is just Javascript

Many people think of jQuery as being different to Javascript however, it is just a library written in Javascript of useful methods and logic.

<br> 

## We Do: Installing jQuery

jQuery is a client side library, which means we need to include it in our HTML. To do this, we have two options:

#### 1. Reference jQuery from a server on the internet

Directly from [jQuery's website](http://code.jquery.com/):

```
 <script src="http://code.jquery.com/jquery-1.11.1.min.js"></script>
```

From a CDN (content delivery network) like [CDNJS](https://cdnjs.com/) or [Google Hosted Libraries](https://developers.google.com/speed/libraries/):

```
 <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
```

What is the benefit of this? Browsers keep a track of the files they have downloaded. If another website also used this CDN file then your browser won't make a request to download the file again which speeds up your website's loading speed.

#### 2. Download a copy of jQuery to host on your own server

[CDNJS](http://www.cdnjs.com), [Google Hosted Libraries](https://developers.google.com/speed/libraries/), and the [jQuery site](http://www.jquery.com) will all allow you to download a copy of jQuery to include in your projects.

<br>

## I Do: Minification

**What's with the 'min.js' in the name of the jQuery file?**

If you look carefully at the filenames of the jQuery versions you download, or just look at the URL in the "src" attribute for each script tag above, you'll notice something at the end of each file name — namely, that they end in 'min.js'. This means the javascript code has been minified.

#### Minified? Did I read that right?

Yep. You did. Minification is the process of making a javascript file smaller by (among other things): 

- Removing all line breaks and whitespace
- Reducing the length of variable and function names
- Stripping out all comments

Minification can significantly reduce the size of a javascript file, and in turn, significantly decrease the time it takes our browsers to load the file into memory.

#### What is the difference?

In jQuery's 1.11.1's case, the original (unminified) code is about 276 kilobytes, whereas the minified code is only 94 kilobytes. That makes the minified version **one-third** the size of the original - not bad!

#### Non-minified

Minified scripts can be difficult to read, so most servers that host jQuery and other libraries will also offer the original (non-minified) version of the code so developers can understand the code.

**Even if you don't fully understand the code, it's a good exercise to visit code.jquery.com and take a look at minified and non-minified jQuery.**

<br>

## I Do: 1.x vs. 2.x jQuery

If you've visited the [jQuery website](http://code.jquery.com), you'll see that there are two major versions in development.

- The **1.x branch** is the most cross-browser-compatible version of the jQuery core.
- The **2.x branch**, while offering some new features, is not compatible with older web browsers — most notably, it's not compatible with Internet Explorer versions 8 and below.

<br>

## I Do: `$` (The Dollar Sign)

Before we get started with jQuery, we should have a look at the `$`. 

The `$` is nothing but an alias for the jQuery library. 

If we have a look at the unminified jQuery code on [Google's CDN](https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.js) we can see at the bottom there is the code:

```
window.jQuery = window.$ = jQuery;
```

Essentially by using either `$` or `jQuery` followed by either a `.` or directly by `()` we can access the methods in the jQuery library.

<br>

## We Do: Document Ready vs DOMContentLoaded

Browsers load from top to bottom. If we want to perform tasks on the DOM, we need to wait until the browser has seen and understood those elements.

In pure javascript, we use `DOMContentLoaded`. The `DOMContentLoaded` event is fired when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading.

jQuery has a similar method to help us wait until the page is ready called: 

```
$(document).ready();
```

### Create an HTML file

Let's make a new HTML page and a JS file and open it in Sublime: 

```
$ touch index.html
$ touch app.js
$ subl .
```

Now let's add some boilerplate code and require jQuery and `app.js`:

```
<!DOCTYPE>
<html>
<head>
  <title>Intro to jQuery</title>
  <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
  <script type="text/javascript" src="./app.js"></script>
</head>
<body>

</body>
</html>
```

**Notice**: We have included the `app.js` at the TOP of the page, in the head BEFORE the `body`.

Now inside the `body`, let's add some html elements:

```
 <div id="container">
   <h1 id="heading" class="text">jQuery is cool</h1>
   <p class="text">jQuery is quite useful</p>
   <p class="text">You are going to like it!</p>
   <p>jQuery is just Javascript</p>
 </div>
```

Let's open that in the browser.

#### Let's be impatient

Let's use pure Javascript to select an element in the body. In `app.js`:

```
console.log(document.getElementById('container'));
=> null
```

#### DOMContentLoaded

Now let's try to make that selection once the DOM has been loaded using DOMContentLoaded:

```
document.addEventListener("DOMContentLoaded", function(event) {
  console.log(document.getElementById('container'));
});
```

Now we should get the DOM element back!

#### Document Ready

Let's now try with jQuery's document ready:

```
$(document).ready(function(){
  console.log(document.getElementById('container'));
});
```

The same!

#### Shorthand Document Ready

There is a shorthand for the document ready:

```
$(function(){
  console.log(document.getElementById('container'));
});
```

#### Named function

You can also pass a named function to `$(document).ready()` instead of passing an anonymous function.

<br>

## We Do: DOM manipulation with jQuery

Let's just think about how we would perform the following tasks with pure javascript:

- **select** a `div` using it's `id`, `class` or html `tagName`

```
var element = document.getElementById(id);
var element = document.getElementsByClassName(className);
var element = document.getElementsByTagName(tagName);
```

- **append** a new `div` with some content to a web page

```
var div = document.createElement('div');
document.body.appendChild(div);
```

- **style** a `div` with a red background

```
div.style.color = 'red';
```

Some of these are quite long. Let's have a look how to do some DOM manipulation in jQuery!

#### Selecting an element with jQuery

(You can practise with `index.html` and the Chrome REPL).

To select an element in the DOM, we use the global jQuery function followed by brackets and then a CSS selector in inverted commas or quotations:

This is the basic syntax for jQuery selections

```
$(' ')
```

To select a particular element by tag (for example `h1` tags), you can do:

```
$('h1');
```

**Note**: What comes back looks like an array.

To select by ID, you use the CSS syntax for an id:

```
$('#container');
```

To select all elements of a particular class, use CSS syntax again:

```
$('.text');
```

You can use more complicated CSS selectors as well:

```
$('p.text');
```

This would selecs all `<p>` tags that also have the class "text" e.g.

```
 <p class="text">jQuery is quite useful</p>
```

<br>

## I Do: A jQuery object?!

#### Variable assignment and selection

If you use variable assignment when doing a selection, a [`jQuery object`](https://learn.jquery.com/using-jquery-core/jquery-object/) is returned.

**Note**: Normal DOM elements have methods and properties, a jQuery object just adds a few more methods and properties to the selected object. Just think about a jQuery object as a supercharged DOM element!

We prepend `$` to variable names when a variable is going to be a jQuery object to help us remember what that variable is for:

```
var $paragraphs = $('p'); 
```

This would return a jQuery object containing all `<p>` tags on your web page.

However, we don't HAVE to prepend '$' to our variables. It's just so we can remember what a variable is being used for:

```
var paragraph = $('p');
```

This is functionally identical to the version above that includes the `$` in front of `paragraph`.

<br>

## We Do: Changing content

Using pure Javascript and the standard DOM API we could change the content of this element:

```
 <h1 id="heading" class="text">jQuery is cool</h1>
```

By doing:

```
var element = document.getElementById('heading');
element.innerHTML = "Javascript is cool!";
```

Even though the pure javascript code above isn't too hard to deal with, in jQuery this is a one-liner:

```
$('#heading').html("jQuery is Cool");
```

If we wanted to **save our selection as a jQuery object**, the code would look like this instead:

- First we select the element we want and save it as a jQuery object:

```
var $heading = $('#heading');
```

- Then we use our jQuery object to perform our task

```
$heading.html("jQuery Objects are Cool!");
````

#### Small summary

There are three things about the example above that make jQuery easier to use:

1. jQuery is using the **same syntax as CSS** to select elements.
2. jQuery allows us to **chain methods** together to accomplish our goals (i.e., $().html(...) ), making code shorter and easier to understand.
3. jQuery deals with any **cross-browser** compatibility issues, which may not seem like a big deal in this example, but which quickly become difficult to deal with as things get more complex.

<br>

## We Do: Changing CSS 

You can do more than select elements and modify content. You can also create or update CSS style attributes in jQuery using the `.css()` method:

```
$("#heading").css("color", "red");
```

The code above will change the color of all text inside the element with the id of "heading" to red.

Or, if we have a bunch of elements that all have the same class (in this example, it's `text`), we can use the class selector to modify the color of all of them at once:

```
$(".text").css("color", "blue");
```

In pure Javascript you would have to loop through each element.

<br>

## Closure

There are SO many things you can do with jQuery, we have just scratched the surface.

You don't HAVE to use it, [you might not need jQuery](http://youmightnotneedjquery.com/).

However, everyone uses it as good programmers are lazy!

**The jQuery Documentation is really good**

The documentation on [jQuery's website](http://code.jquery.com/) is really good. It has great examples.

### Questions

Any questions?

<br>

