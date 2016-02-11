---
layout: post
title: "Why I Love JS Bin"
date: 2014-05-28 11:11:07
---
{% raw %}
I used to use [JS Bin](http://jsbin.com/) just because it was easy to get an ember gist started at [emberjs.jsbin.com](http://emberjs.jsbin.com). Then slowly I started to become partial to its styling over [jsFiddle](http://jsfiddle.net)/[codepen](http://codepen.io)/etc., but that is just a personal preference. But now I love JS Bin because it knows a little more about me, how I work, and with what technologies.

I would imagine that other online editors have similar options to the ones I am about to describe, so if you prefer those, then you should probably find the similar features as well and make use of them, because then things get _AWESOME_!

##Step 1: LOGIN!!
This may seem unnecessary in most cases but the important part is that once you login then you can customize your experience, and in the case of JS Bin you can customize a decent amount!

##Creating a default template
Check out my default JS Bin template as of right now:
<a class="jsbin-embed" href="http://emberjs.jsbin.com/rovib/1/embed?html,js,output">Ember/Coffee/Emblem/Data Starter Kit</a><script src="http://static.jsbin.com/js/embed.js"></script>

The first cool trick I started taking advantage of once I logged in was creating a template. Before that, I was using handlebars and javascript in JS Bin and then having to convert it all to emblem/coffeescript whenever I pulled snippets into my project's source.

Basically what I did was took the default emberjs.jsbin.com template and manually converted it to emblem and coffeescript and then clicked _File -> Save as template_. Done!  Now every time I create a new JS Bin I'm already in my normal context!

By default emberjs.jsbin.com does not use ember-data. For problems with anything but the simplest level of complexity ember-data seems to become necessary for my purposes. Every time I needed to add ember-data to my JS Bin it was a little more of a chore than I would like, so I decided to just convert the `["red", "yellow", "blue"]` model to use `DS.FixtureAdapter` instead. One _File -> Save as template_ later and I never had to drag in ember-data again!

##Editor settings
This is where things start to get _REALLY_ cool. I am a VIM user, so one of the things that annoyed the most about switching between JS Bin and my project's source was constantly switching between VIM and normal keybindings. Well, apparently I was doing this for no reason at all because JS Bin actually supports VIM mode as well as a number of other cool features like themes!

Check out your editor settings here: [jsbin.com/account/editor](http://jsbin.com/account/editor).

##Preferences
If you're like me, you could care less about what your styles look like in a JS Bin, and when you create a new JS Bin you want to immediately focus on the JavaScript panel and get started.

Every time I would create a new JS Bin I would toggle the CSS panel and then click on the JavaScript panel.

Well now I don't have to do that any longer, check out your preferences here and customize things to your workflow: [jsbin.com/account/preferences](http://jsbin.com/account/preferences).

##Open Source
Maybe one of the coolest features that I recently found with JS Bin is that it is [open source](https://github.com/jsbin/jsbin). This means that I can actively contribute to making it even better!
{% endraw %}
