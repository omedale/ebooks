![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Intro to CSS
=====

##Opening

If HTML is a set of instructions telling the browser WHAT to display, CSS tells it HOW to display it. 

CSS stands for: 

- **C**ascading 
- **S**tyle 
- **S**heet

It provides the browser with precise instructions on how to style each element we want displayed on the page. 

It can affect the text format (font, size, color, etc.), the size and position of various objects on the page, etc. 

<br>

##I Do: CSS Syntax

We build our CSS with a selector (usually the name of the html tag, but it can also be a specific class of elements, or an element with a unique ID):

#### Draw on board

```
selector {
  property_1: value_1;
  property_2: value_2;
}
```

Do not forget the curly brackets, or the semi-colon after the value! 

The last semi-colon can be omitted but to be honest, don't worry about that.

<br>

##We Do: Let's do some CSS

Let's create a new html page:

```
$ mkdir css-basics && css-basics
$ touch css-basics.html
```
	
Then let's create a basic html structure:

```
 <!DOCTYPE>
 <html>
   <head>
	 <title>Intro to CSS</title>
   </head>
 <body>
 </body>
 </html>
```

#### Inline CSS

We can style a tag inline like this:

```
<body style="background:red">
```

Open in browser.

However, this is BAD for lots of reasons. Don't do this!

###We Do: Linking the stylesheet to the html file

Inside the `<head>` tags, we need to add a self-closing `<link>` tag, indicating the type of relations (`rel="stylesheet"`) and the file path (`href="style.css"`):

```
<link rel="stylesheet" href="style.css">
```

We often have a specific folder for stylesheets, as we can have several on one application. For now, we placed the style.css file within the same folder as our html file, making it easy to target it (`href="style.css"`)

#### We need to create a css file

```
touch style.css
```

<br>

##We Do: Let's do some CSS

#### Add some html

First, we need to add some html to style:

```
 <p>This is a paragraph element</p>
	
 <div>This is a DIV</div>
 <div>This is another DIV</div>
```

Now, let's add some CSS into our stylesheet file:

```
p {
  color: orange;
}
```

This will change the color of ALL paragraph tags to have the font-color "orange".

Refresh the page.

```
div {
  border: 1px solid black;
}
```

This will add a 1px black border to each DIV on the page, since the selector targets the "div" elements.

Refresh the page.

#### CSS Comments

To comment out something in CSS, we use ```/* ... */``` syntax.

Example:

```
div {
  /* border: 1px solid black; */
}
```
	
#### Shortcut CSS properties

Some CSS properties you can join together. For example:

```
div {
  /* border: 1px solid black; */
  border-width: 1px;
  border-style: solid;
  border-color: black;
}
```
  
#### Some more

You can also change the background color of elements ("background-color"), as well as the color of the text contained in these elements ("color"). Be careful not to confuse the two!

```
div {
  /* border: 1px solid black; */
  border-width: 1px;
  border-style: solid;
  border-color: black;
  background-color: blue;
  color: white;
  width: 100px;
  height: 50px;
}
```

<br>

### We Do: "id" and "class" attributes in CSS

We can apply "class" and "id" attributes to elements in html. It allows us to target these specific elements in CSS.

#### IDs

Ids are used when you have one example of something on a page. Not one example of an HTML tag, but one specific element you want to make unique.

Let's have a look at an example of using IDs:

In our HTML file: 

```
 <div id="div_1">
   ...some content...
 </div>

 <div id="div_2">
   ...some content...
 </div>

 <div id="div_3">
   ...some content...
 </div> 
```

Now within our "style.css" file:

```
#div_1 {
  background-color: green;
}
```

This allows us to target specific elements on the page (here, only the div with the ID "div_1"). We can give any name we want to our ID attribute (besides the obvious reserved words, such as tag names, etc.).

#### Classes

The class attribute allows us to target not one, but several elements that may share similarities. 

Add: 

```
 <div id="div_1">
   <div class="red_bg">
     ...some content...
   </div>
   <div class="red_bg">
     ...some content...
   </div>
 </div>
```

Now within our "style.css" file:

```
.red_bg {
  background-color: red;
} 
```

We can also do:

```
#div_1 .red_bg {
  background-color: red;
} 
```
	
If we want to be more specific.

<br>

##We Do: Text-align

Let's add another p tag, and align the text to the right of the screen. 

```
 <p class="text-align">Align this right</p>
```
	
Let's add some css:

```
.text-align {
  text-align: right;
}
```

By applying this class to elements in our HTML file, we can position the text they contain on the right. 

<br>

##We Do: Changing the font

We can change the font, using

	.text-align {
	  text-align: right;
	  font-family: "Comic Sans MS";
	}

By applying this class to elements in our HTML file, we can apply this particular font to targeted elements. 

We have used a web-font, one that the browser already works with. However you can add custom fonts using [Google Fonts](http://www.google.com/fonts/) or you can include your own font.

<br>

##We Do: Hiding elements

We can hide elements using css by:

```
.text-align {
  text-align: right;
  font-family: "Comic Sans MS";
  visibility: hidden;
}
```

This will hide the targeted element, but the space where it should be on the page still exists.

If we don't want this, we can do:

```
.text-align {
  text-align: right;
  font-family: "Comic Sans MS";
  /*visibility: hidden;*/
  display: none;
}
```

This will not only hide the targeted element, but also remove it completely from the flow of the page, getting rid of the place that was allocated for it.

<br>

##We Do: Multiple classes

You can also chain classes together, applying several classes to one element:

Let's add:

```
 <p class="first second">Multiple classes</p>
```

Then lets create two classes:

```
.first {
  font-size: 40px;
}

.second {
  color: red;
}
```

As we can imagine, the possibilities are endless. There are many properties and values to work with, and many ways to target specific elements. Two pages could have the same HTML content, and yet look dramatically different, due to different CSS stylesheets.

<br>

## I Do: Specificity in CSS

One of the most important concepts with CSS is specificity. Every element gets a score and it's this score that dictates which CSS property is applied.

[Specificity Calculator](http://specificity.keegan.st/)

<br>

##Closure

CSS is really fun to do. You have to remember a few rules but once you have them remembered, it's greate to see things change in front of your eyes.

<br>

###Questions

Any questions?

<br>