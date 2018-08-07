![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Chrome Developer Tools
=====

## Opening

The Chrome Developer Tools (DevTools for short), are a set of debugging tools built into Google Chrome. 

We can do a lot of useful things using these tools but some of the key ones are:

- HTML & CSS as the browser understands them
- Requests being made and received
- Javscript being run
- Amongst other things

Really, we are very lucky to have such a powerful set of browser tools at our disposal!

<br>

## We Do: Accessing the DevTools

First, let's navigate to [http://www.google.com](http://www.google.com).

Now to access the DevTools, we can press:

- `cmd+alt+i` to open the DevTools (will open on the last tab you had open)
- `cmd+alt+j` to open the DevTools on the console tab
- `cmd+shift+c` to open the DevTools with the inspector

<br>

## I Do: DevTools Tabs

Overall, there are eight main tools available in the Developer Tools. You may see people with a few more as you can add custom ones using extensions.

![developer-tools](https://cloud.githubusercontent.com/assets/40461/8398454/82d1523c-1de6-11e5-94b0-f5390a4ed124.jpg)

- [**Elements**](https://developer.chrome.com/devtools/docs/dom-and-styles): Editing Styles And The DOM
- [**Resources**](https://developer.chrome.com/devtools/docs/resource-panel): Managing application storage
- [**Network**](https://developer.chrome.com/devtools/docs/network): Evaluating network performance
- **Sources**: A graphical interface to the V8 debugger
- [**Timeline**](https://developer.chrome.com/devtools/docs/timeline): Performance profiling with the Timeline
- [**Profiles**](https://developer.chrome.com/devtools/docs/profiles): Profile the execution time and memory usage of a web app or page. 
- **Audits**: The Audit panel can analyze a page as it loads.
- [**Console**](https://developer.chrome.com/devtools/docs/console): The JavaScript Console 

We won't use all of these tabs during the course, the key ones we are going to get very familiar with are:

- **Elements**
- **Network**
- **Console**

<br>

## We Do: Elements Tab

You can use the Elements panel for a variety of tasks:

- Inspecting the HTML & CSS of a web page.
- Test different layouts.
- Live-edit CSS.

Let's have a play with some of these tools.

### Change the background of Google

- Press `cmd+shift+c` to open the inspector view 
	- You can also do this by pressing the magnifying glass
	- Or right-clicking on the page and selecting "Inspect Element" at the bottom
- Select the whole body.
- Look at the DOM nodes on the left hand side
- Look at the CSS responsible for a rendered element in the browser.

When you are sure that you have the body selected, in the CSS live editor add:

```
element.style {
  background: red;
}
```

#### Tips

- Notice that as you start typing background, the css properties autocomplete
- If you press `shift` and click on the coloured box, you can see that the color changes format RGBA, Hex etc
- If you click on the coloured box, you will also see a colour selector
- If you drag your mouse onto the screen, you also get a colour selector!

Inside this CSS editor, you can also:

- Copy and past styles
- Use up/down arrow to increment/decrement values by one. 
- Use `alt+↑` or `alt+↓` to inc/dec by 0.1. 
- Use `shift+↑` or `shift+↓`to inc/dec by 10.

### Change Dom element

Inside the DOM tree view, we can see a representation of the Document Object Model as interpreted by the browser.

We can edit these elements. 

- Select the `body` element
- Delete it by pressing the `Delete` button
- Then Undo this by pressing `cmd+z`

#### Tips

- We can copy & pase elements with `cmd+c` & `cmd+v`
- We can edit the HTML contents, if we `right-click` and choose "Edit as HTML"

### CSS Computed Tab

In the CSS Tab, aside from seeing the CSS properties for any inspected element. We can also see a visual representation of the box model along with the computed values.

<br>

## We Do: Network Tab

The Network panel records information about each network operation in your application, including detailed timing data, HTTP request and response headers, cookies, WebSocket data, and more. 

- Refresh the page and have a look at the requests being made by the page.
	- Notice that the status of a lot of the resources are **304** (not modified)
- Select 'Disable Cache' so the requests new from the server each time.
	- Refresh the page, and you should see that everything is now **200** (ok)
	
### Filtering

By default, the network Tab shows all requests being made. However, you can filter these requests by:

- All
- XHR
- Script
- Style
- Images
- Media
- Fonts
- Documents
- WebSockets
- Other

You can also search through these requests, which can be useful.

#### Tips

If you hover over an image in the network tab, you can right click and `Copy as cURL`

In the terminal, paste the cURL information and add `-O` (capital O).

```
cd ~/Desktop
curl 'https://ssl.gstatic.com/s2/oz/images/notifications/spinner_64_b6a3129c3429eba076483f2c93ba38f6.gif' -H 'pragma: no-cache' -H 'accept-encoding: gzip, deflate, sdch' -H 'accept-language: en-US,en;q=0.8' -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.124 Safari/537.36' -H 'x-chrome-uma-enabled: 1' -H 'accept: image/webp,*/*;q=0.8' -H 'cache-control: no-cache' -H 'authority: ssl.gstatic.com' -H 'referer: https://plus.google.com/' -H 'x-client-data: CJW2yQEIpLbJAQiptskBCMS2yQEI7ojKAQiRksoB' --compressed -O
``` 

Now you can download images in your terminal a little easier.

<br>

## We Do: Console Tab

Lastly, let's have a look at the console tab `cmd+alt+j`.

The JavaScript Console provides two primary functions for developers testing web pages and applications. It is a place to:

- Log diagnostic information in the development process using [Console API](https://developer.chrome.com/devtools/docs/console-api)
- A shell prompt which can be used to interact with the document and DevTools.

We use a commands like `console.log()` to log values from our Javascript as it executes.

### Shell

The console shell allows us to execute Javascript and also interact with the DOM using Javascript.

Let's try this:

```
> 1 + 1
< 2

> var a = 1;
< undefined

> a
< 1
``` 

#### Debugging

We can also use the Chrome console to debug our code. However, we are going to look at this in a little more detail in a seperate lesson on Debugging.


<br>

##Closure

There are a lot more things that Chrome can do for you. However, we don't have time to look at them in more detail. You will become very familiar with this browser over the course of WDI.

More [shortcuts](https://developer.chrome.com/devtools/docs/shortcuts).

###Questions

Any questions?

<br>