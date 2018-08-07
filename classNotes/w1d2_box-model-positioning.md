![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

CSS Box Model and Positioning
=====

##Opening

Now that we have covered the basics of CSS, let's cover a few of the more tricky elements. 

<br>

## I Do: CSS Box Model

All HTML elements can be considered as boxes. In CSS, the term "box model" is used when talking about design and layout.

The CSS box model is essentially a box that wraps around HTML elements, and it consists of: margins, borders, padding, and the actual content.

The box model allows us to place a border around elements and space elements in relation to other elements. 

With CSS properties and values, it is possible to apply specific styles to each of these elements, and change the way they behave and/or display on the page. 

The image below illustrates the box model:

![box-model](https://cloud.githubusercontent.com/assets/40461/8234473/196b96b4-15d4-11e5-8782-0a8adacd471a.gif)

What do these different layers mean, and how are they relating to one another?

* **Margin** - Clears an area around the border. The margin does not have a background color, it is completely transparent

* **Border** - A border that goes around the padding and content. The border is affected by the background color of the box

* **Padding** - Clears an area around the content. The padding is affected by the background color of the box

* **Content** - The content of the box, where text and images appear

<br>

##We Do: Display

We can display our elements in several different ways. One CSS property, "display", can take on several values that help us in this process: "block", "inline", and "inline-block". 

* An **inline** element has no line break before or after it, and it tolerates HTML elements next to it. (Think a line of text).

* A **block** element has some whitespace above and below it and does not tolerate any HTML elements next to it.

* An **inline-block** element is placed as an inline element (on the same line as adjacent content), but it behaves as a block element.

To illustrate this, let's look at a few exaples, with different display properties:

Continuing from the last CSS basics lesson, add: 
	
```
 <div class="inline">Content</div>
 <div class="inline">Content</div>
 <div class="inline">Content</div>
	
 <div class="block">Content</div>
 <div class="block">Content</div>
 <div class="block">Content</div>
	
 <div class="inline-block">Content</div> 
 <div class="inline-block">Content</div> 
 <div class="inline-block">Content</div> 
```

The css:

```
.inline {
  display: inline;
}

.block {
  display: block;
}

.inline-block {
  display: inline-block;
}
```

![display](https://cloud.githubusercontent.com/assets/40461/8234494/4468a47e-15d4-11e5-828a-c46f3aa125ce.jpg)

<br>

##We Do: Positioning

Another CSS property, "position", can take "*relative*" or "*absolute*" values, among others. 

A page element with "relative positioning" gives you the control to "absolutely position" children elements inside of it. This might not be obvious to everyone - that's probably because this isn't intuitive. At all. Let's look at an example.

![css position relative](https://lh5.googleusercontent.com/1Rg2JABratNT6dc_ykEeZWH3BRhbgwI7JOl45jeqE-IxPUq2bx_xY_jYJQHqi38czuuQIGUqArhfZndC2SOtube_qDZe5h0wWz2xRlRNX-uiwjOfvz2K-Ld7Iw)

The relative positioning on the parent is what matters here. This what would happen if we forgot that:

![](https://lh3.googleusercontent.com/w2-DIT10v5D-5l5BQPnwBp5nmcLhKvfDeJfU-vYpx1l_73dnanrvsDoN0Z4cobGmEv1N5WEEo8XZ5WrK6UU9q87Iwi1AT9WgFeBy6qD8-AG2VrNLHaDmqTPsXA)

In this small example, it doesn't seem to matter much. But it really is a significant change.

⇒ The "absolutely positioned" elements are positioning themselves in relation to the body element, instead of their direct parent. So if the browser window grows, that element in the bottom left is going to stick with the browser window, not hang back inside, like it was the case in the previous example.


**Static Positioning**

HTML elements are positioned static by default. A "static positioned" element is always positioned according to the normal flow of the page.

Static positioned elements are not affected by the top, bottom, left, and right properties.

**Fixed Positioning**

An element with fixed position is positioned relative to the browser window.

It will not move even if the window is scrolled.

**Float**

Float is one of the CSS properties that really confuses people.

The float property specifies whether or not a box (or an element) should float, whether elements should float around it.

![float](https://cloud.githubusercontent.com/assets/40461/8234489/3b61ef02-15d4-11e5-8864-435fb6e0c3cc.png)

Note that "absolutely positioned" elements ignore the float property as they are removed from the normal document flow.

Floated elements remain a part of the flow of the web page. This is distinctly different than page elements that use absolute positioning. 

There are four valid values for the float property. "Left" and "right" float elements those directions respectively. "None" (the default) ensures the element will not float and "inherit" which will assume the float value from that elements parent element.

**Clear**

All elements will float next to floated items until they are specificall cleared. Think about the text on the page.

![clear](https://cloud.githubusercontent.com/assets/40461/8234478/287c1156-15d4-11e5-9901-ba9090a5bf70.png)


<br>