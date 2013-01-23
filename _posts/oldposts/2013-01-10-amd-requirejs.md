---
layout: post
category: JavaScript
tags: amd, javascript, RequireJS
title: AMD & RequireJS
author: nicolasmbatista
---

Hi everyone, this is my first post here! So I encourage you to be comprehensive with my bad writing skills :)

That being said, let’s start!

In this post, I’ll give you a first glance about modules in javascript, and a library to load them, RequireJS, so you can keep your code modularized and loading faster than ever!

So, AMD, is not what you are thinking (Advanced Micro Devices), it actually stands for Asynchronous Module Definition. AMD definitions makes your modules faster to load, organizes your app, and let’s you load modules only when you need them.

I suggest you read [this presentation](http://unscriptable.com/code/Using-AMD-loaders/#6) about AMD as it helps you understand what is it, and how you can use it.

But no worries, I’ll explain that too!

How we define a javascript module using AMD? is super easy, this is a simple module:

{% highlight js %}
define(
    [
        'depA',
        'depB',
        'depC'
    ],
    function (depA, depB, depC) {
        var myModule = {};
        // build your module here
        myModule.foo = depA.getFoo();
        return myModule;
    }
);
{% endhighlight %}

To define a module, you need:

* To define a dependency list (or not), that needs to be load in order to use this module.
* And to define your javascript module. Just create a function, with the dependencies as parameters, and then return your module so it can be use from outside

That’s it!

Now that we have our module working, let’s learn how to load it, and that’s where require comes in.

In order to load a module, with its dependencies, asynchronously and only when you really need it, you need to use require as this:

{% highlight js %}
require(
    ["modA", "modB"],
    function (modA, modB) {
        // do something with modA and modB
        // when they are fully loaded
    }
);
{% endhighlight %}

To load a module, you need:

* To ask for what modules you need using require
* Once they are loaded, use them!!

Yup, that’s it.

Notice that the function using the modules, is a callback function, that means, it won’t execute until all modules finished loading.

Now let’s see some actual code.

First, you need to download [RequireJS](http://requirejs.org/).

Once you downloaded it, create an `index.html` with a head that looks like this:

{% highlight html %}
<!DOCTYPE html>
<html>
  <head>
    <title>Using RequireJS</title>
    <!-- we reference requirejs and tell it that what we want to load is specified in data-main -->
    <script data-main="scripts/main" src="scripts/require.js"></script>
  </head>
  <body>
  </body>
</html>
{% endhighlight %}

In this simple expample, our Structure is very very super! basic.

{% highlight js %}
Project
Project/index.html
Project/scripts
Project/scripts/require.js
Project/scripts/main.js
Project/scripts/movie.js
{% endhighlight %}

Let’s take a look at main.js

{% highlight js %}
// Here we are loading a "movie" module to use in our callback function
require(["movie"], function(Movie) {
    var a = new Movie();
	  a.setAttribute('name','terminator');
	  console.log(a.getAttribute('name'));
});
{% endhighlight %}

As we said before, we ask require for the modules we want to use (`movie`) and create a callback function (`function(movie)`) to use it. Here we are just seting its name to "terminator", since is an awesome movie.

Now let’s take a look at movie.js

{% highlight js %}
define("movie", function () {
  //Constructor
	var Movie = function () {
	};
 
	//Private vars and functions
	var attributes = {};			
	Movie.prototype = {
		constructor : Movie
		,getAttribute : function (key){
			return attributes[key];
			}
 
		,setAttribute : function (key,value){
				attributes[key] = value;
			}				
	};
	return Movie;
});
{% endhighlight %}

Let’s see the code:

First, we declare our dependencies (in this case, since we don’t have any, we just ommit them), then, we have the option to declare a module with a name. In this case I called it movie. And after that, the declaration of the module itself.

There are a few ways to do this, but to make the post shorter, I’ll explain one, using `constructor`, `prototype`, `private vars`, etc.

{% highlight js %}
//Constructor
    var Movie = function () {
};
{% endhighlight %}

This code just creates a variable, called Movie, of type function, so it takes its prototype.

After that, we create a simple private variable that we’ll use as a hash table.

{% highlight js %}
//Private vars and functions
var attributes = {};
{% endhighlight %}

And then, we extend the prototype of the Movie variable.

We specify its constructor function (Wich is called Movie if you remember). After that we add two methos to set and get the values from our private variables.

{% highlight js %}
Movie.prototype = {
  constructor : Movie
	,getAttribute : function (key){
		return attributes[key];
	}
	,setAttribute : function (key,value){
			attributes[key] = value;
	}			
};
{% endhighlight %}

And once we are done, we return our module:

{% highlight js %}
return Movie;
{% endhighlight %}

There are several discussion topics in the last code, I encourage you to read about [prototypes](http://javascriptweblog.wordpress.com/2010/06/07/understanding-javascript-prototypes/) if you are interested on how they work.
And Here is my github [code](https://github.com/nicolasmbatista/startup/tree/master/04-amd-requirejs) that shows something very similar to what is shown on this post

Ok that’s it for today, I hope I didn’t bored you to death and see you next time!