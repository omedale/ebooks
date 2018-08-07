![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Responsive Design
=================
[i]: Download the latest Chrome version (optional).

## Opening: What is responsive design?

> "Responsive Design" is the strategy of making a site that "responds" to the browser and device that it is being shown on... by looking awesome no matter what.

Or, the dryer Wikipedia definition:

> Responsive web design (RWD) is a web design approach aimed at crafting sites to provide an optimal viewing experience—easy reading and navigation with a minimum of resizing, panning, and scrolling—across a wide range of devices (from mobile phones to desktop computer monitors).

#### More devices

Not that long ago building a successful online presence meant just ensuring that your website worked correctly in all the major desktop browsers. 

Fast forward to today (2015) and the desktop computer is dying, more than 61% of the UK population owns a smartphone.

- **195 million** tablet devices were sold in 2013.
- The number of active mobile devices and human beings crossed over somewhere around the [7.19 billion mark](http://www.independent.co.uk/life-style/gadgets-and-tech/news/there-are-officially-more-mobile-devices-than-people-in-the-world-9780518.html).
- New devices like iWatches are changing the game too

<br>

## I Do: Mobile is the future

> "Having a mobile friendly website is no longer just important, it’s critical." 

[Forbes Ecommerce Marketing Checklist for 2013](http://www.forbes.com/sites/brentgleeson/2013/03/14/ecommerce-marketing-checklist-for-2013/)

<br>

## I Do: How to do Responsive Design wrong

The MAIN way of doing Responsive Design wrong is not to plan for it. Changing a web-platform to mobile is much harder thand changing mobile to web.

#### Examples of non-responsive sites:

Everytime I teach this lesson, it is becoming harder and harder to find non-responsive websites... I keep having to change the list!

- [Apple](https://www.apple.com/uk/) (Okay on mobile but not great)
- [Amazon](https://www.amazon.co.uk/) (A site designed specifically for mobile)
- [Huffington Post](http://www.huffingtonpost.co.uk/) (A specific mobile site)

Aside: When this was last run (12 weeks ago, these weren't) but now they have been updated: 

- [HMRC](http://www.hmrc.gov.uk/)

Open these up and resize the page.

#### Examples of responsive sites:

- [Boston Globe](http://www.bostonglobe.com/)  
- [GA](https://generalassemb.ly/)
- [Metro](http://metro.co.uk/) Good example!

What's the difference between these? Let's resize again.
Interestingly, **Boston Globe was the first example of a responsive website.**

Instead of manually resizing the page which can be a pain we can use tools like this:

- [Brad Frost](http://bradfrostweb.com/demo/ish/)

Add a url into the input box (top left).

You can easily resize the screen and play around and see how the differnt sites look like using the buttons on the top right.

If you are really bold, choose disco!

<br>

## I Do: Responsive Design tools

There are a number of other stand alone tools that you can use.

- [Ghostlab](http://vanamco.com/ghostlab/)

#### Chrome's new developer tools

With the latest Chrome update, there is a really cool new tool in the development tools. 

- Click on the device icon next to the magnifying glass.
- You can change the pixel width (displayed at the top) using the drag tool.
- You can select any device using the dropdown menu at the top.

#### Xcode

Another great tool is the Xcode simulator.

<br>

## We Do: Make a responsive website

[i]: Create from scratch or send over starter code

```
mkdir responsive_site && responsive_site
mkdir js
mkdir stylesheets
touch index.html
touch stylesheets/reset.css
touch stylesheets/style.css
touch js/app.js
```

Now open everything in Sublime and add the contents of a [reset.css](http://cssreset.com/) to the reset stylesheet.

#### Add some HTML

Now let's add some html into the index.html file:

```
<!DOCTYPE html>
<html>
<head>
  <title>Responsive design</title>
  <link href='http://fonts.googleapis.com/css?family=Montserrat:400,700' rel='stylesheet' type='text/css'>
  <script type="text/javascript" src="./js/app.js"></script>
  <link rel="stylesheet" type="text/css" href="./stylesheets/reset.css">
  <link rel="stylesheet" type="text/css" href="./stylesheets/style.css">
</head>
<body>
  <header>
    <nav>
      <ul>
        <li><h1>Responsive Design</h1></li>
        <li>Like normal design, but responsive.</li>
        <li><span>So many</span> devices</li>
        <li>
          <ul>
            <li><a href="/">Desktop</a></li>
            <li><a href="/">Phone</a></li>
            <li><a href="/">iPad</a></li>
            <li><a href="/">iWatch</a></li>
          </ul>
        </li>
      </ul>
    </nav>
  </header>
  <main>
    <div class="column">
      <h2>Exciting content</h2>
      <p>Web development is so fun...</p>
    </div>
    <div class="column">
      <h2>More content</h2>
      <p>Device testing is quite tedious...</p>
    </div>
    <div class="column">
      <h2>Even more content</h2>
      <p>But it has to be done now...</p>
    </div>
  </main>
</body>
</html>
```

#### Add some CSS

```
*{
  box-sizing: border-box;   
  margin: 0px;  
  padding: 0px;  
} 
    
body {
  font-family: 'Montserrat', sans-serif;
  color: black;
}

header, main {
  width: 960px;
  margin: 0 auto;
  position: relative;
}

/* HEADER */

header nav ul li {
  overflow: hidden;
}

header nav > ul > li:nth-child(1) h1 {
  color: rgb(242, 138, 40);
  text-transform: uppercase;
  font-weight: 700;
  font-size: 88px;
}

header nav > ul > li:nth-child(2) {
  height: 35px;
  padding: 0 10px;
  font-size: 23px;
  line-height: 35px;
  color: #ffc719;
  background: black;
}

header nav > ul > li:nth-child(3) span {
  color: #ff0044;
  text-transform: uppercase;
  font-weight: 700;
  padding: 10px;
  font-size: 25px;
  display: inline-block;
}

header nav > ul > li:nth-child(4) {
  background: rgb(241, 241, 241);
  margin-bottom: 15px;
}

header nav > ul > li:nth-child(4) ul li {
  display: inline;
}

header nav > ul > li:nth-child(4) a {
  padding: 15px;
  display: inline-block;
  color: black;
  text-decoration: none;
}

header nav > ul > li:nth-child(4) a:hover {
  background: #ffc000;
}

/* MAIN COLUMNS */
main .column h2 {
  padding: 15px;
  color: white;
}

main .column:nth-child(1) h2 { background: rgb(126, 211, 33);}
main .column:nth-child(2) h2 { background: rgb(235, 91, 76); }
main .column:nth-child(3) h2 { background: rgb(0, 174, 255); }

main .column p {
  padding: 15px;
}
```

<br>

## We Do: Make the columns responsive

How do we go about splitting these columns across the page?

Where the CSS for the columns have been defined (at the bottom) let's add:

```
main .column {
  float: left;
  width: 33.33%;
}
```

#### Adjusting the container width 

Let's resize the page... Nothing. This is because the contain element has a fixed width. Let's change the css for the main selector:

```
header, main {
  max-width: 960px;
  margin: 0 auto;
  position: relative;
}
```

Let's test!

It works, however the text gets squished. This will not look good when there is lots to read.

#### Setting a min-width

Let's set a min-width instead to prevent this:

```
main .column {
  float: left;
  width: 33.33%;
  min-width: 320px;
}
```

When there is not enough space for the 320px element to fit, it will now flow underneath the element to it's left, starting from the right to the left.

#### Why 320px?  

That's the width of an iphone 3G.

Okay, so that looks good when the screen is small and large but what about in the middle?

<br>

## We Do: Media queries

In order to target specific device/screen sizes we need to use media-queries.

As there are lots of different devices, there can be lots of different media-queries.

- [CSS-Tricks](https://css-tricks.com/snippets/css/media-queries-for-standard-devices/) has a good resource for media-queries

One way of doing this is by including `media` in your stylesheet link.

```
<link rel='stylesheet' media='screen and (min-width: 701px) and (max-width: 900px)' href='css/medium.css' />
```
But this is not very cool. A better way is to include in your CSS. This is the syntax:

#### Max-width 960px

```
@media only screen and (max-width: 960px) {  
} 
```

This will apply style only when this condition is true.

We include this at the bottom of the page.

```
@media only screen and (max-width: 960px) {  
  main .column {
    width: 50%;
  }
  main .column:last-child {
    width: 100%;
  }
}
```

Specificity still applies. So if we didn't add `main` then this still wouldn't be as specific as the one above.

#### Max-width 640px

This looks good when the window is greater than 640px however we need to add one more media query for when the window is smaller than this.

```
@media only screen and (max-width: 640px) { 
  main .column {
    width: 100%;
  }
}
```

Let's test! Great!

<br>

## We Do: Style the header

Our columns are now working but we need to do a little bit of work on our header.

Sometimes, with responsive design we have to decide to omit content from a site. This can sometimes mean that we are loading content on the mobile device that the user can't see (which will slow down their page) however, for this case we will not worry about that.

```
@media only screen and (max-width: 960px) { 
  header nav ul li {
    display: none;
  }
  
```

If we resize the page, everything in the header disappears. Let's just show the first li with the header and the last one with the menu:

```
@media only screen and (max-width: 960px) {  
  header nav ul li {
    display: none;
  }

  header nav > ul > li:nth-child(1),
  header nav > ul > li:nth-child(4) {
    display: block;
  }
}
```

This is a little better.

#### Title

Now we want the title to change size depending on the browser size. Let's do the middle size first:

```
@media only screen and (max-width: 960px) {  
  header nav ul li {
    display: none;
  }

  header nav > ul > li:nth-child(1),
  header nav > ul > li:nth-child(4) {
    display: block;
  }

  header nav > ul > li:nth-child(1) {
    text-align: center;
    padding: 30px 0;
  }

  header nav > ul > li:nth-child(1) h1 {
    font-size: 40px;
  }
}
```

Now let's do the smaller browser:

```
@media only screen and (max-width: 640px) { 
  header nav > ul > li:nth-child(1) {
    padding: 15px 0;
  }

  header nav > ul > li:nth-child(1) h1 {
    font-size: 30px;
  }
}
```


<br>

## We Do: Menu

The issue we have is the menu. When we get to a small size, there isn't enough room for all of the links. 

#### Add burger icon

We are going to have to add a new "burger icon". There are a number of different ways to do this. We are going to do this with a text icon. Let's add another li to the nav ul:

```
 <li>
	<ul>
      <li><a href="#"></a></li>
      <li><a href="/">Desktop</a></li>
      <li><a href="/">Phone</a></li>
      <li><a href="/">iPad</a></li>
      <li><a href="/">iWatch</a></li>
    </ul>
  </li>
```

And let's style this with CSS.

```
@media only screen and (max-width: 640px) {
  .
  .
  .
  
  header nav > ul > li:nth-child(4) ul li:nth-child(1) {
    float: right;
    display: block;
  }

header nav > ul > li:nth-child(4) ul li:nth-child(1) a:before { 
    content:'\2630';
  }
  
  .
  .
  .
}
```

Let's have a look at this. All of the li's will be block level.

Now we want to hide all of the lis except the first one and make the links 100%:

```
@media only screen and (max-width: 640px) {
  .
  .
  .
  
  header nav > ul > li:nth-child(4) ul li {
    display: none;
  }
  
  header nav > ul > li:nth-child(4) ul li a {
    width: 100%;
  }
  .
  .
  .
}
```

Now we need to add some jQuery to make the navigation bar slide up and down.

First we need to add jQuery into the index.html

```
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
  <script type="text/javascript" src="./js/app.js"></script>
```

Now let's add some jQuery to app.js

```
$(function(){
  $('header nav > ul > li:nth-child(4) ul li:nth-child(1)').on('click', function(){
    event.preventDefault();
    $(this).siblings().slideToggle();
  });
})
```

So now, we should have a responsive site!

Note: If you get some issues with when the browser window changes size, you might need to add some !important tags to make sure that the browser uses the right selector.


<br>

## I Do: Responsive images & tables

Images and tables are often difficult when doing responsive design. 

Images sometimes stretch or "squish" so `max-width` is your friend. Sometimes it may be more sensible to serve different images for different devise sizes, a 1200px image doesn't make sense to load on a mobile devise. 

We're not going to go through this now but it is something to consider.

<br>

## We Do: On your phone

Well if we want to check out the site we'd have to upload the file to a webserver.  We probably don't all have sites and it is probably a pain.  So let's run a little server from our computers and check out our site on our phones.

Run the following in the folder where you saved your index.html  

``` 
python -m SimpleHTTPServer  
```

To check it out on your computer go to:

```
http://0.0.0.0:8000
```

Great you are running a simple web server.  We could have put this index.html page into a rails app and run that but that would be overkill.

If you are on the same wifi network on your computer and your phone you can check out the site on your phone.  First we need the ip address of our computer.

Type in `ifconfig` in the terminal. There should be something like:

```
inet 10.0.1.85
```

On your phone if you goto: 

```
http://10.0.1.85:8000
```

and you should see your awesome website.....

#### Meta viewport

Doh... it will probably look like it does on our desktop.

Mobile's are clever - they pretend they have a width of 960px and scale the website.  We need to overide this and force the mobile to respond to our media queries.

Put the following code into our header.

```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

##Closure

Summary of the lesson.

<br>

###Questions

Any questions?

<br>