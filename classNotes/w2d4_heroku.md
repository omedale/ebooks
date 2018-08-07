![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

Deploying to Heroku
=====

## Opening

When we have finished developing a version of our app, we might want to put it on the internet for other people to see.

#### Localhost

Most of what we've developed so far has just run on our own computers. Both our database and our web server have been on our computer. We've done this because it's much easier to develop locally so we don't need an internet connection.

However, people can't access it easily unless they are also on our local network.

#### Buy a computer

We could just rent another computer somewhere else to run our apps (or even more than one). We could connect it to the internet and with a bit of configuration, we could allow people to connect to it using a URL.

However, we'd have to buy and look after this computer, have somewhere to store it and ensure that it was working and always connected to the internet. Also, if someone hit an error when they used our app, we might have to stop and start it? Maybe there is a better way? 

#### Virtual machines

What if we could write a program that pretends to be a computer? If we could do this, then we could run another operating system within it? This is called a virtual machine.

#### Cloud hosting platorm

Heroku is a cloud-based service. Essentially it's virtual machines that run on Amazon Web Services (EC2).

To deploy an app to Heroku, it's a fairly straightforward step-by-step process.

First you need to link your machine to your Heroku account - a similar process to what we did with Github.

<br>

## We Do: Add SSH-key to Heroku

Very similar to when we setup Github, we need to add our ssh-keys to Heroku so that Heroku can know that it can authenticate us.

So let's add our ssh-key to Heroku. First, we need to copy our ssh-key:

```
cat ~/.ssh/id_rsa.pub | pbcopy
```

Then we need to go to [Heroku](https://www.heroku.com/). 

Email > Manage Account > SSH Keys.

<br>

## We Do: Install Heroku Toolbelt

Next we need to install the [Heroku Toolbelt](https://toolbelt.heroku.com).

This is a command-line tool that allows us to use command, similar to the way that we used git on our computer.

Once it is installed, you need to login with your heroku credentials:

```
$ heroku login
Enter your Heroku credentials.
Email: adam@example.com
Password (typing will be hidden):
Authentication successful.
```

<br>

## We Do: Deploy a HTML & JS project

Let's make a small app so that we can deploy it to Heroku:

You must make sure that you are not in a git tracked repo.

```
$ mkdir first-app
cd first-app
```

#### Git init

Heroku works with git, so you need to git init this directory:

```
$ git init
```

#### Create some files

Let's create some files so that we can see something on our website:

```
$ touch index.html
$ mkdir js 
$ mkdir css
$ touch js/app.js
$ touch css/style.css
```

Open in Sublime:

```
$ subl .
```

Inside the `index.html` file let's add some boilerplate code:

```
<!DOCTYPE>
<html>
<head>
  <title>My First Live Website</title>
  <script type="text/javascript" src="./js/app.js"></script>
  <link rel="stylesheet" type="text/css" href="./css/style.css">
</head>
<body>
  <h1>My First Live Website</h1>
</body>
</html>
```

Inside `style.css` let's make the background of the body red:

```
body {
  background: red;
}
```

Inside `app.js` let's fire an alert:

```
alert("loaded");
```

#### Git add & commit

Now you need to add all the files:

```
git add -A
git commit -m "First commit"
```

#### Heroku create

Now you need to create a new app on Heroku using the heroku cli:

```
heroku create
```

You wil get a message similar to:

```
Creating boiling-ravine-9951... done, stack is cedar-14
https://boiling-ravine-9951.herokuapp.com/ | https://git.heroku.com/boiling-ravine-9951.git
Git remote heroku added
```

<br>

## We Do: Use php? 

Heroku is primarily aimed at apps running on frameworks, like Ruby on Rails, Django (Python), node.js, or… ahem… PHP.

For static [`ruby`](https://devcenter.heroku.com/articles/static-sites-ruby) sites on Heroku you still need to do a little bit of configuration.

Howver, heroku allows you to publish PHP sites as well, with NO configuration needed! That’s right, just create your .php files, and it will figure out that the Heroku app should run PHP for this site, and it will auto-configure the app to run on the latest version of PHP/Apache.

### So here is how you do it:

Rename your `index.html` to `home.html` or something similar.

```
$ mv index.html home.html
```

Create an index.php file:

```
$ touch index.php
```

Add some php to include the home.html file

```
$ echo > index.php "<?php include_once('home.html'); ?>"
```

#### Git add & commit

Now we can add these new files:

```
$ git add -A
$ git commit -m "Setting up php file"
```

#### Heroku push

Now you can push to heroku with this commad:

```
$ git push heroku master
```

When you push, you will see:

```
Counting objects: 10, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (10/10), 924 bytes | 0 bytes/s, done.
Total 10 (delta 0), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote: 
remote: -----> PHP app detected
remote: 
remote:  !     WARNING: No composer.json found.
remote:        Using index.php to declare PHP applications is considered legacy
remote:        functionality and may lead to unexpected behavior.
remote: 
remote: -----> No runtime required in composer.json, defaulting to PHP 5.6.10.
remote: -----> Installing system packages...
remote:        - PHP 5.6.10
remote:        - Apache 2.4.10
remote:        - Nginx 1.6.0
remote: -----> Installing PHP extensions...
remote:        - zend-opcache (automatic; bundled)
remote: -----> Installing dependencies...
remote:        Composer version 1.0.0-alpha10 2015-04-14 21:18:51
remote: -----> Preparing runtime environment...
remote:        NOTICE: No Procfile, using 'web: vendor/bin/heroku-php-apache2'.
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote: 
remote: -----> Compressing... done, 72.6MB
remote: -----> Launching... done, v3
remote:        https://boiling-ravine-9951.herokuapp.com/ deployed to Heroku
remote: 
remote: Verifying deploy... done.
To https://git.heroku.com/boiling-ravine-9951.git
 * [new branch]      master -> master
```

#### Scale dyno

You will need to tell Heroku to use a dyno to serve the website:

```
$ heroku ps:scale web=1
```

#### Heroku open

And you can open the website with:

```
$ heroku open
```

<br>

## We Do: Further configuration

This is a very simple way to deploy a static site. We can define many more options however we will look at this when we deploy a server application.

<br>

##Closure

Summary of the lesson.

<br>

###Questions

Any questions?

<br>
