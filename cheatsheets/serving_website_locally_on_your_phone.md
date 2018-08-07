Seeing your website on your phone
------------------------------------

Well, if we want to check out the site we'd have to upload the file to a webserver.  We probably don't all have sites and it is probably a pain.  So let's run a little server from our computers and check out our site on our phones.

Run the following in the folder where you saved your index.html  
``` 
python -m SimpleHTTPServer  
```

To check it out on your computer go to:

http://0.0.0.0:8000

Great you are running a simple web server.  We could have put this index.html page into a rails app and run that but that would be overkill.

If you are on the same wifi network on your computer and your phone you can check out the site on your phone.  First we need the ip address of our computer.

Type in ifconfig in the terminal. There should be something like:

inet 10.0.1.85

On your phone if you goto 

http://10.0.1.85:8000

and you should see your awesome website.....

doh... it will probably look like it does on our desktop.

Mobile's are clever - they pretend they have a width of 960px and scale the website.  We need to overide this and force the mobile to respond to our media queries.

Put the following code into our header.

```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

##RAILS
To view your rails app in your phone, launch your rails server then type `ifconfig` in a seperate terminal window. Be sure to add `:3000` instead of `:8000` to the end of your path since that's your default rails server port.